# Introduction
PSRFM is a program developed to interpolate high resolution images based on a high resolution (landsat/sentinel) image before and after the date, along with 3 low resolution MODIS images on the same days as the original high resolution image, and one on the day desired for prediction. It is originally a C++ Program.

This application simplifies the process of running PSRFM into a single-input procedure, and also reduces the peak computing power necessary to run PSRFM by splitting the images into smaller tiles and processing them individually.

# Setup
- A python 3 environment is required with the packages included in the packages.txt file in this repository (conda recommended)
- Create a google account and register it for Google Earth Engine here https://signup.earthengine.google.com/#!/
- Using the google account created above, download google drive's backup and sync here and make sure it's syncing with your local filesystem https://www.google.com/intl/en_ca/drive/download/
- Install Jupyterlab
- Clone this repository 

# Execution
- Create an input json file in the same format as the sample inputs (more detail below) with all the appropriate information and save it into the same directory as this base repo. 
  - Leave fields "skip_if_reference_not_found", "overlap_fraction" and "percent_cloudy" alone unless you want to edit some specific parameter:
    - skip_if_refrence_not_found: if set to false, the code will not finish execution if reference images cannot be found for a single tile.
    - overlap_fraction: determines how much overlap there is between tiles to allow space for the program to sufficiently crop images for PSRFM
    - percent_cloudy: determines the maximum amount of cloud cover that is permissible for a reference image to be valid, increase if no images are being found for a significant amount of tiles but note that quality of output may reduce on cloudier tiles
  - longs and lats: Enter 4 coordinates of a square or rectangle for the area to be processed
  - date_range: Enter the range of dates (YYYY-DD-MM) for which you want to find reference images within (minimum 3 weeks recommended). Expand this if too many tiles are coming up empty.
  - prediction_dates: Insert all the dates for which you want images for within the Date Range.
  - satellite_choice: Insert the choice of satellite to generate the high res images in the format of:
    - landsat 8: ls8
    - landsat 5: ls5
    - sentinel 2: s2
  - drive_folder: To execute PSRFM, images need to be downloaded to your google drive, insert the folder name into which you would like them downloaded into, choose a unique one for every execution or clear the folder in your google drive before executing something with the same name twice. Once a PSRFM run has been completed and output has been generated, feel free to delete folder and it's contents within your google drive if space is a concern.
  - local_drive_folder_location: Include the absolute path of where the google drive backup and sync folder is located.
  - local_dst_base_path: Include the absolute path of where you would like the output of PSRFM to be placed
- Open full_PSRFM_runner.ipynb in jupyterlab, and in the 7th cell, insert the name of the json input you have created ![image](https://user-images.githubusercontent.com/65920380/120159722-7f181400-c1c3-11eb-9601-58776c6b9c89.png)
- Execute the whole notebook
- A prompt will come up to authorize Earth Engine, enter the credentials for the google account used to register for earth engine in the Setup section, and enter the code provided, then close the tab.![image](https://user-images.githubusercontent.com/65920380/120159844-a4a51d80-c1c3-11eb-83fc-d5a593526c87.png)

- Execution will complete, and output images will be found in the directory specified in the input json

# Sample Inputs
2 Sample execution files are included in the home directory (Sample_LS8.json and Sample_S2.json) for Landsat 8 and Sentinel 2 respectively
