% List of image file names
imageFiles = ["a.jpg", "R.jpg", "dhruv.jpg","nani.jpg"]; % Add more file names as needed

% Create a loop to process each image
for i = 1:numel(imageFiles)
    % Read the image
    theImage = imread(imageFiles(i));
    [width, height] = size(theImage);

    if width > 320
        theImage = imresize(theImage, [320 NaN]);
    end 

    % Perform face detection
    faceDetector = vision.CascadeObjectDetector();
    locationOfFaces = step(faceDetector, theImage);

    % Check if any faces are detected
    if ~isempty(locationOfFaces)
        % Draw rectangles around the detected faces
        detectedImage = insertShape(theImage, "rectangle", locationOfFaces);

        % Display the image with detected faces
        figure;
        imshow(detectedImage);
        title('Faces Detected!');
    else
        disp('No faces detected in this image.');
    end
end
