% This MATLAB program takes in a series of images from a folder, and prompts the
% user to designate regions of interest (ROIs).  The two ROIs create masks
% that allow for the segmentation of one image into three regions.  These
% new images are then output to a new folder. 

inputFolder = 'C:\Users\btyle\Desktop\PUMP\ProliferationMatLab\newImgs';
if ~isfolder(inputFolder)
    errorMessage = sprintf('Error: folder DNE');
    inputFolder = uigetdir();
    if inputFolder == 0
        return;
    end
end

outputFolder = 'C:\Users\btyle\Desktop\PUMP\ProliferationMatLab\newDisected';
if ~isfolder(outputFolder)
    errorMessage = sprintf('Error: folder DNE');
    outputFolder = uigetdir();
    if outputFolder == 0
        return;
    end
end

filePatternInput = fullfile(inputFolder, '*.tif');
theFilesInput = dir(filePatternInput);

for i = 1: 1%length(theFilesInput)
    baseFileNameInput = theFilesInput(i).name;
    fullFileNameInput = fullfile(theFilesInput(i).folder, baseFileNameInput);
    description = 'Uterus Tissue';
    titleName = strcat(description, baseFileNameInput);
    
    img = imread(fullFileNameInput);
    
    muscleMaskedImg = img;
    connectiveMaskedImg = img;
    mucosaMaskedImg = img;
    
    muscleConnectiveBinaryMask = img;
    connectiveMucosaBinaryMask = img;
    
    connectiveOuterMaskedImg = img; % placeholder for incomplte connective tissue
    
    done = true;
    while(done) % create muscle tissue img & muscle and connective tissue border
        
        imshow(img);
        axis on;
        
        % Set up figure properties:
        % Enlarge figure to full screen.
        set(gcf, 'Units', 'Normalized', 'OuterPosition', [0 0 1 1]);
        
        % Name title bar
        set(gcf, 'Name', titleName, 'NumberTitle', 'Off');
        
        % Prompt user for ROI
        message = sprintf('Draw the border that defines the muscle and connective tissue \nAdjust ROI accordingly \nExit window when done');
        uiwait(msgbox(message));
        roi = drawassisted();
        
        muscleConnectiveBinaryMask = roi.createMask();
        
        waitfor(roi); 
        
        % Prompt user to redo or continue
        promptMsg = sprintf('Click yes to move to connective and mucosa border \nClick no to recalibrate border');
        button = questdlg(promptMsg, 'whatever', 'Continue', 'Recalibrate', 'Quit', 'Continue');
        
        if strcmpi(button, 'Continue')
            
            % create muscle tissue dissection
            muscleMaskedImg = bsxfun(@times, img, cast(~muscleConnectiveBinaryMask, 'like', img));
            imshow(muscleMaskedImg);
            waitfor(imshow(muscleMaskedImg));
            
            % save img to folder
            tissueType = '_Muscle';
            outputFileName = baseFileNameInput(1:end-4);
            outputBaseFile = strcat(outputFileName, tissueType, '.tiff');
            outputFullFile = fullfile(outputFolder, outputBaseFile);
            imwrite(muscleMaskedImg, outputFullFile);
            done = false;
            
        elseif strcmpi(button, 'Quit')
            msgbox('The program has been exited. \nAll completed images have been saved to the output folder.');
            exit;
        elseif strcmpi(button, '')
            msgbox('The program has been exited. \nAll completed images have been saved to the output folder.');
            exit;
        else
            done = true;
        end
        
    end
    
    done = true;
    while(done) %create border between connective and mucosa tissue
        
        % create img w/ area outisde connective tissue removed
        connectiveOuterMaskedImg =  bsxfun(@times, img, cast(muscleConnectiveBinaryMask, 'like', img));
        
        % Set up figure properties:
        % Enlarge figure to full screen.
        set(gcf, 'Units', 'Normalized', 'OuterPosition', [0 0 1 1]);
        % Name title bar
        set(gcf, 'Name', titleName, 'NumberTitle', 'Off');
       
        imshow(connectiveOuterMaskedImg);
        axis on;
        
        % Prompt user for ROI
        message = sprintf('Draw the border that defines the connective and mucosa tissue \nAdjust ROI accordingly \nExit window when done');
        uiwait(msgbox(message));
        roi = drawassisted();
        
        connectiveMucosaBinaryMask = roi.createMask();
        
        waitfor(roi);

        % Prompt user to redo or continue
        promptMsg = sprintf('Click yes to move to next image \nClick no to recalibrate border');
        button = questdlg(promptMsg, 'Yes', 'No');
        
        if strcmpi(button, 'Yes')
            
            connectiveMaskedImg = bsxfun(@times, connectiveOuterMaskedImg, cast(~connectiveMucosaBinaryMask, 'like', connectiveOuterMaskedImg));
            imshow(connectiveMaskedImg);
            waitfor(imshow(connectiveMaskedImg)); %can be taken out once code is complete
            
            % save img to folder
            tissueType = '_Connective';
            outputFileName = baseFileNameInput(1:end-4);
            outputBaseFile = strcat(outputFileName, tissueType, '.tiff');
            outputFullFile = fullfile(outputFolder, outputBaseFile);
            imwrite(connectiveMaskedImg, outputFullFile);
            
            done = false;
        else
            done = true;
        end
        
        % create mucosa tissue dissected img
        mucosaMaskedImg = bsxfun(@times, img, cast(connectiveMucosaBinaryMask, 'like', img));
        imshow(mucosaMaskedImg);
        waitfor((imshow(mucosaMaskedImg))); %can be removed after code is finished
        
        % save img to folder
        tissueType = '_Mucosa';
        outputFileName = baseFileNameInput(1:end-4);
        outputBaseFile = strcat(outputFileName, tissueType, '.tiff');
        outputFullFile = fullfile(outputFolder, outputBaseFile);
        imwrite(mucosaMaskedImg, outputFullFile);
        
        %consider user prompts in command window to give option to escape
        
     end
         
 end
