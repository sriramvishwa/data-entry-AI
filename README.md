Data entry project - image to excel conversion
The web application allows users to upload an image, specify parameters, and download the processed files.

Image

Upload Image: A file input for uploading a picture.
Number of Chunks: Enter a text field to indicate how many chunks the image should be divided into.
Number of Records: The number of records can be entered using this text field.
Processing Mode: "Image Chunking Only" and "Image Chunking & OCR" are selected via a dropdown menu.
Prefix for the Output File Name: A text field for the output file name prefix.
Process and Download Button: This button initiates the processing of the form after it is submitted.

Code description:
The web application is made using the Flask web framework.
Shell commands execute in a subprocess.
Configuration values are imported from a configuration file, such as OCR_API_URL and OCR_API_KEY.
To process the photos, import the functions get_excel_from_image and download_image_chunks.

Application Setup for Flask:
Template_folder and static_folder are initialized to "templates" in the Flask application.
Route for Webhooks:

A bash script is used to retrieve the most recent changes from the server via a POST route called /update_server.
Principal Pathway (/):

Both GET and POST methods are supported by the route.
It renders the upload form (upload_form.html) in response to a GET request.
It handles the submitted picture on a POST request by using the parameters that have been chosen.

Processing of Images:

Retrieved are the uploaded image and form data (chunk count, record count, processing choice, and output file name prefix).
The get_excel_from_image function is triggered if the "Image Chunking & OCR" option is used. It chunks and OCRs the image and then produces a zip file with the Excel files that are produced.
The download_image_chunks function is triggered if the "Image Chunking Only" option is chosen. It splits the image into chunks and generates a zip file with the picture chunks within.
Following processing, the zip file is made available for download along with the relevant headers.
The Flask application runs in debug mode if the script is executed directly.

Workflow
User Interaction:
The user accesses the form via the web browser.
They upload an image file, specify the number of chunks and records, choose a processing mode, and provide a file name prefix.
They click the "Process and Download" button.

Form Submission:
The form data is sent to the server via a POST request.
The server processes the image based on the selected options.

Processing:
If "Image Chunking Only" is selected, the image is divided into chunks, which are then zipped and returned to the user.
If "Image Chunking & OCR" is selected, the image is divided into chunks, OCR is performed on each chunk, and the results are compiled into Excel files, which are then zipped and returned to the user.

Download:
The user receives a zip file containing the processed results.

This setup allows for flexible processing of images for data entry projects, providing either simple image chunking or a combination of chunking and OCR to convert images to structured Excel files.
