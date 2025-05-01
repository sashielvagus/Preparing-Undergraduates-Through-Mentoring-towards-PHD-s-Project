%%% This function segments and quantifies leaf area. The code will
%%% extract an image from a file, segment the leaves, quantify the area,
%%% and return the area. The images here are extracted from a folder so
%%% there are extra inputs to accommodate for the directory


function areas = colorAreaCalculator(NumberOfImages, thresholdFunction, proliferation , nonproliferation, show, start)


%%% Allowing this many inputs gives a generic code that can be used for any
%%% group of any sample size. 

%%% The threshold is an input function using ColorThresholding App.

format long g;
format compact;
fontSize = 20;

if nargin<6
    show = false;
end

if nargin<7
    start = 1;
end

FolderSize = NumberOfImages;
areas = zeros(FolderSize - start + 1,7); 

%change file paths per personal use
inFolder = 'folder path';
if ~isfolder(inFolder)
    errorMessage = sprintf('Error: folder DNE');
    inFolder = uigetdir();
    if inFolder == 0
        return;
    end
end

%change file paths per personal use
outFolder = 'folder path';
if ~isfolder(outFolder)
    errorMessage = sprintf('Error: folder DNE');
    outFolder = uigetdir();
    if outFolder == 0
        return;
    end
end

filePattern = fullfile(inFolder, '*.tiff');
theFiles = dir(filePattern);

for j = 1: 2%length(theFiles)  % you can specify 
    baseFileName = theFiles(j).name;
    fullFileName = fullfile(theFiles(j).folder, baseFileName);
    
    % read the image and store the pixel values (color) in the matrix rgbImage
    rgbImg = imread(fullFileName);
    
    % Threshold using created function
    % Convert RGB image to chosen color space
    mask = thresholdFunction(rgbImg);
    
    maskproliferation = proliferation(rgbImg);
    maskNonproliferation = nonproliferation(rgbImg);

    % Extract biggest blob.
    %mask = bwareafilt(mask, 1);
    
    % Fill holes.
    %mask=imfill(mask,'holes');

    
    if show == true
        
        
        figure(j);
        subplot(2,3,1);
        %Display original image
        imshow(rgbImg);
        title('Original RGB Image', 'FontSize', fontSize, 'Interpreter', 'None');

        %Display total area mask
        subplot(2,3,2);
        imshow(mask)
        title('Tissue Mask', 'FontSize', fontSize, 'Interpreter', 'None');
        % Mask the image using bsxfun() function
        %maskedRgbImage1 = bsxfun(@times, rgbImg, cast(mask, 'like', rgbImg));
        
        
        %Display Proliferation Mask
        subplot(2,3,3);
        imshow(maskproliferation)
        title('Proliferation Mask', 'FontSize', fontSize, 'Interpreter', 'None');
        % Mask the image using bsxfun() function
        maskedRgbImage2 = bsxfun(@times, rgbImg, cast(maskproliferation, 'like', rgbImg));
        
        %Display NonProliferation Mask
        subplot(2,3,4);
        imshow(maskNonproliferation)
        title('NonProliferation Mask', 'FontSize', fontSize, 'Interpreter', 'None');
        % Mask the image using bsxfun() function
        maskedRgbImage3 = bsxfun(@times, rgbImg, cast(maskNonproliferation, 'like', rgbImg));
        
        % Display RGB proliferation cells
        subplot(2,3,5);
        imshow(maskedRgbImage2)
        title('Proliferation Cells RGB', 'FontSize', fontSize, 'Interpreter', 'None');
        
        % Display RGB non proliferation cells 
        subplot(2,3,6);
        imshow(maskedRgbImage3)
        title('NonProliferation Cells RGB', 'FontSize', fontSize, 'Interpreter', 'None');

        % Set up figure properties:
        % Enlarge figure to full screen.
        set(gcf, 'Units', 'Normalized', 'OuterPosition', [0 0 1 1]);
        
        % Get rid of tool bar and pulldown menus that are along top of figure.
        titleName = "Uterus Gland " + baseFileName;
        % Give a name to the title bar.
        set(gcf, 'Name', titleName, 'NumberTitle', 'Off');
        

    end
    
        
    % compute the number of pixels that are not zero (Area)
    pxlmm = 20.7261;
    areas(j-start+1, 1)  = nnz(mask)/ (pxlmm^2); %total area of tissue
    areas(j-start+1, 2) = nnz(maskproliferation) / (pxlmm^2); % area of proliferating cells
    areas(j-start+1, 3) = nnz(maskproliferation) / nnz(mask); % ratio of proliferating cells to total area
    areas(j-start+1, 4) = (nnz(maskproliferation) / nnz(mask))*(100); % ratio of prolif. cells as PERCENTAGE
    areas(j-start+1, 5) = nnz(maskNonproliferation) / (pxlmm^2); %area of non proliferating cells
    areas(j-start+1, 6) = nnz(maskNonproliferation) / nnz(mask); 
    areas(j-start+1, 7) = (nnz(maskNonproliferation) / nnz(mask))*(100); % ratio of non prolif. cells as PERCENTAGE
    
    outBaseFile = sprintf(baseFileName);
    outFullFile = fullfile(outFolder, outBaseFile);
    %figure(j); %activate the figure again 
    export_fig(outFullFile); %export figures to output folder
    %imwrite(fig(j), outFullFile);
    
end

end
