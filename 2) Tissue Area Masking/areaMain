% This code takes in a series of histology images and analyzes the area of
% cells based on color in respect to the area of the entire tissue being
% analyzed. This is achieved through color thresholding, and the creation
% of masks that focus on the distinction of brown (proliferating cells) and
% blue (non proliferating) cells in a pig uterus tissue.

clc;    % Clear the command window.
close all;  % Close all figures (except those of imtool.)
clear;  % Erase all existing variables. Or clearvars if you want.
workspace;  % Make sure the workspace panel is showing.

%retrieve num of images in folder
d = dir('*.tiff');  
numOfImgs = length(d);  %are these necessary? where are they used??

areas = colorAreaCalculator(1, @totalTissueAreaMask, @proliferationMask , @nonProliferationMask, true, 1);
%tissueName = getTissueNameCol(string);

% output results into excel sheet
% following folder name must be created on desktop
filename = 'FileName.xlsx';
