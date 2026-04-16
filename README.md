# New Version Released! [here](https://github.com/DIVYESH-HARI/PlantCare-AI-Version-2)
# PLANTCARE AI - DISEASE DETECTION SYSTEM
# Installation & Configuration Guide


INTRODUCTION
------------
PlantCare AI represents an advanced solution for plant disease identification utilizing:
- YOLO (You Only Look Once) technology for disease classification
- Real-ESRGAN for supplementary image enhancement
- Streamlit framework for the web interface

Capable of identifying 15+ diseases affecting tomatoes, potatoes, and peppers, complete with 
professional treatment guidance.

SYSTEM SPECIFICATIONS


BASELINE REQUIREMENTS:
- Python 3.12 or newer
- 8 GB RAM minimum
- 5 GB available disk space
- Windows 10/11, Linux, or macOS

OPTIMAL CONFIGURATION:
- Python 3.12
- 16 GB RAM
- NVIDIA GPU with 6GB+ VRAM
- 10 GB available disk space (SSD preferred)


SETUP INSTRUCTIONS

STEP 1: EXTRACT THE ARCHIVE
----------------------------
Extract the downloaded archive to your preferred location.

Example:
    C:\PlantCare-AI\

Post-extraction, you should observe:
    - Real-ESRGAN/                    (Image enhancement component)
    - Image Segmentation_Plant Disease/  (YOLO model and datasets)
    - real.py                         (Primary application file)
    - requirements.txt                (Python dependencies)
    - README.txt                      (This document)


STEP 2: INSTALL REQUIRED PACKAGES
----------------------------------
Launch Command Prompt or Terminal in the extracted directory and execute:

    pip install -r requirements.txt

This command installs all necessary Python packages.
NOTE: Installation duration may range from 5-10 minutes based on connection speed.


STEP 3: CONFIGURE REAL-ESRGAN
------------------------------
Navigate to the Real-ESRGAN folder and perform installation:

    cd Real-ESRGAN
    python setup.py develop
    cd ..

This installs Real-ESRGAN in development configuration.


STEP 4: LAUNCH THE APPLICATION
-------------------------------
From the main directory, start the application:

    streamlit run real.py

The interface will launch automatically in your default browser at:
    http://localhost:8501


TROUBLESHOOTING GUIDE


ISSUE 1: ImportError with rgb_to_grayscale
-------------------------------------------
ERROR MESSAGE:
    ImportError: cannot import name 'rgb_to_grayscale' from 
    'torchvision.transforms.functional_tensor'

RESOLUTION:
1. Identify your Python environment's site-packages directory:
   
   FOR ANACONDA:
   C:\ProgramData\anaconda3\envs\[YOUR_ENV_NAME]\Lib\site-packages\
   
   FOR STANDARD PYTHON:
   C:\Python3X\Lib\site-packages\
   
   FOR VIRTUAL ENVIRONMENT:
   [YOUR_VENV_PATH]\Lib\site-packages\

2. Navigate to: basicsr\data\degradations.py

3. Open the file using a text editor (Notepad, VSCode, etc.)

4. Locate the line:
   from torchvision.transforms.functional_tensor import rgb_to_grayscale

5. Modify it to:
   from torchvision.transforms.functional import rgb_to_grayscale

6. Save changes and restart the application

ALTERNATIVE (Locate exact path):
    python -c "import basicsr; print(basicsr.__file__)"


ISSUE 2: Streamlit Command Not Recognized
------------------------------------------
ERROR MESSAGE:
    'streamlit' is not recognized as an internal or external command

RESOLUTION:
    pip install --upgrade streamlit
    
OR utilize:
    python -m streamlit run real.py


ISSUE 3: Model Files Cannot Be Located
---------------------------------------
ERROR MESSAGE:
    FileNotFoundError: YOLO model not found

RESOLUTION:
Verify all paths in real.py are accurate. Open real.py and confirm the
configuration section aligns with your installation directory:

    config = {
        "REALESRGAN_PATH": r"C:\PlantCare-AI\Real-ESRGAN",
        "MODEL_REALESRGAN_PATH": r"C:\PlantCare-AI\Real-ESRGAN\weights\RealESRGAN_x4plus.pth",
        "YOLO_MODEL_PATH": r"C:\PlantCare-AI\Image Segmentation_Plant Disease\Yolov11 Variants for PDP\best.pt",
        "HEALTHY_IMAGES_PATH": r"C:\PlantCare-AI\Image Segmentation_Plant Disease\healthy"
    }


ISSUE 4: CUDA Memory Exhausted
-------------------------------
ERROR MESSAGE:
    RuntimeError: CUDA out of memory

RESOLUTIONS:
- Deactivate image enhancement (uncheck the enhancement option in the interface)
- Upload smaller images (pre-resize if necessary)
- Terminate other GPU-intensive applications
- Switch to CPU processing mode


ISSUE 5: Port Conflict
-----------------------
ERROR MESSAGE:
    Address already in use

RESOLUTION:
Specify an alternative port:
    streamlit run real.py --server.port 8080

USER GUIDE


BASIC WORKFLOW:
1. Launch: streamlit run real.py
2. Upload an image file (JPG, JPEG, or PNG)
3. Optional: Activate enhancement for lower-quality images
4. Click "Analyze Plant"
5. Review results and treatment recommendations

OPTIMIZATION TIPS:
- Utilize clear, well-illuminated images
- Focus on foliage displaying symptoms
- Avoid blurred or low-resolution photographs
- Activate enhancement only for suboptimal quality images


IDENTIFIED DISEASES


TOMATO (9 conditions):
- Bacterial Spot
- Early Blight
- Late Blight
- Leaf Mold
- Septoria Leaf Spot
- Spider Mites (Two-spotted spider mite)
- Target Spot
- Yellow Leaf Curl Virus
- Mosaic Virus

POTATO (2 conditions):
- Early Blight
- Late Blight

PEPPER (1 condition):
- Bacterial Spot


ALTERNATIVE CONFIGURATION WITH ANACONDA


CREATE ENVIRONMENT:
    conda create -n plantcare python=3.12
    conda activate plantcare

INSTALL PACKAGES:
    pip install -r requirements.txt

CONFIGURE REAL-ESRGAN:
    cd Real-ESRGAN
    python setup.py develop
    cd ..

LAUNCH APPLICATION:
    streamlit run real.py


ALTERNATIVE CONFIGURATION WITH VIRTUAL ENVIRONMENT

CREATE VIRTUAL ENVIRONMENT:
    python -m venv venv

ACTIVATE (Windows):
    venv\Scripts\activate

ACTIVATE (Linux/Mac):
    source venv/bin/activate

INSTALL PACKAGES:
    pip install -r requirements.txt

CONFIGURE REAL-ESRGAN:
    cd Real-ESRGAN
    python setup.py develop
    cd ..

LAUNCH APPLICATION:
    streamlit run real.py


ADVANCED SETTINGS


MODIFY PORT:
    streamlit run real.py --server.port 8080

RESTRICT UPLOAD SIZE (in MB):
    streamlit run real.py --server.maxUploadSize 5

ENFORCE CPU MODE:
    Edit real.py and modify:
    device = torch.device('cpu')

ENFORCE GPU MODE:
    Edit real.py and modify:
    device = torch.device('cuda')

COMMON ERROR RESOLUTIONS

ERROR                          | RESOLUTION
-------------------------------|------------------------------------------
Module not found               | Execute: pip install -r requirements.txt
CUDA error                     | Update NVIDIA drivers or switch to CPU mode
Port already in use            | Use: --server.port 8080
Model loading failure          | Verify and update paths in real.py
Memory exhausted               | Deactivate enhancement or resize images
Streamlit not found            | Execute: pip install --upgrade streamlit
Import error (rgb_to_grayscale)| Modify degradations.py as documented above

SUPPORT & CONTACT INFORMATION


For issues, inquiries, or assistance, please reach out to the authors:

PROJECT AUTHORS:
Divyesh Hari G
- Email: divyesh02208@gmail.com
- GitHub: https://github.com/DIVYESH-HARI

Vijaya Karthick
- Email: vkr3056@gmail.com
- GitHub: https://github.com/KARTHICK-3056

Vishnu Vardhan
- Email: skvishnu2006@gmail.com

VERSION DETAILS


Version: 1.0.0
Release Date: January 1, 2025

CAPABILITIES:
- YOLO-powered disease identification
- Real-ESRGAN 4x image enhancement
- 15+ disease classifications
- Professional treatment recommendations
- Contemporary web interface with Streamlit


ACKNOWLEDGMENTS


- Ultralytics: YOLO object detection framework
- Xintao Wang et al.: Real-ESRGAN image enhancement
- Streamlit: Web application framework
- All contributors to this project


Developed with dedication for healthier agricultural outcomes.


