<!-- PROJECT SHIELDS -->
<!--
*** I'm using markdown "reference style" links for readability.
*** Reference links are enclosed in brackets [ ] instead of parentheses ( ).
*** See the bottom of this document for the declaration of the reference variables
*** for contributors-url, forks-url, etc. This is an optional, concise syntax you may use.
*** https://www.markdownguide.org/basic-syntax/#reference-style-links
-->
[![Mentor][mentor-shield]][mentor-url]
[![Issues][issues-shield]][issues-url]
[![MIT License][license-shield]][license-url]

# Face Alignment and Face Swap ![image](https://github.com/anilbhatt1/Deep_Learning_EVA4_Phase2/blob/master/S1_MobileNet_AWS_Lambda_S3_Insomnia/aws.jpg)
________

<!-- TABLE OF CONTENTS -->
## Table of Contents

* [Prerequisites](#prerequisites)
* [License](#license)
* [Group Members](#group-members)
* [Mentor](#mentor)
* [Approach](#Approach)
* [Face Alignment](#face-alignment)
* [Face Swamp](#face-swap)
* [Webpage](#webpage)

        
## Prerequisites

* [Linux](https://www.tutorialspoint.com/ubuntu/index.htm)
* [Python 3.8](https://www.python.org/downloads/) or Above
* [AWS Account](https://aws.amazon.com/free/?all-free-tier.sort-by=item.additionalFields.SortRank&all-free-tier.sort-order=asc)
* [Serverless](https://www.serverless.com/) 
* [Insomnia](https://insomnia.rest/download/)
* [Google Colab](https://colab.research.google.com/)
* [Open-CV](https://pypi.org/project/opencv-python/)

<!-- LICENSE -->
## License

Distributed under the MIT License. See `LICENSE` for more information.

<!-- GROUP MEMBERS -->
## Group Members
  - [Gajanana Ganjigatti](https://github.com/gaju27) , [Gaju_on_LinkedIn](https://www.linkedin.com/in/gajanana-ganjigatti/)
  - [Anilkumar N Bhatt](https://github.com/anilbhatt1) , [Anil_on_LinkedIn](https://www.linkedin.com/in/anilkumar-n-bhatt/)
  - [Maruthi Srinivas](https://github.com/mmaruthi) , [Maruthi_on_LinkedIn](https://www.linkedin.com/in/maruthi-srinivas-m/)
  - [Sridevi B](https://github.com/sridevibonthu) , [Sridevi_on_LinkedIn](https://www.linkedin.com/in/sridevi-bonthu/)
  - [SMAG TEAM](https://github.com/SMAGEVA4/session1/tree/master/Session1) :performing_arts: team github account

<!-- MENTOR -->
## Mentor

* [Rohan Shravan](https://www.linkedin.com/in/rohanshravan/) , [The School of A.I.](https://theschoolof.ai/)

<!-- APPROACH -->
## Approach

1. Create an S3 bucket
2. Upload to S3 bucket - 5-point landmark.dat, js folder, index.html & error.html.
3. Go to Ubuntu
4. Check if existing environment created for S1 & S2 will suffice. If anything additional or downgrading is required, better to create a dedicated environment for S3 alone with these specific requirements.
5. If not required, activate old environment (S1_mobilenet) itself & proceed.
6. Prepare handler.py in such a way that it points to correct buckets & correct model_paths we chose from web.
    Option Chosen from web : Resnet34 Classifier -> Should pick S3_BUCKET eva4p2-s1-anilbhatt1 -> MODEL_PATH s1_resnet34.pt
    Option Chosen from web : MobileNet_V2 Classifier -> Should pick S3_BUCKET eva4p2-s2-anilbhatt1 -> MODEL_PATH s2_mobilenetv2.pt
    Option Chosen from web : Facealignment  -> Should pick S3_BUCKET eva4p2-s3-anilbhatt1 -> MODEL_PATH shape_predictor_5_face_landmarks.dat
7. Below section in handler.py will need modification to achieve point 6
    Define environment variables if they are not existing
    S3_BUCKET = os.environ['S3_BUCKET'] if 'S3_BUCKET' in os.environ else 'sridevi-session1-bucket'
    MODEL_PATH = os.environ['MODEL_PATH'] if 'MODEL_PATH' in os.environ else 'session1mobilenet.pt'
8. We will also need to modify below function in handler.py to get back 'Aligned Face' image
    `def get_prediction(image_bytes):
      tensor = transform_image(image_bytes = image_bytes)
      return model(tensor).argmax().item()`

9. Deploy lambda function using serverless, get the url for face alignment.

10. Modify upload.js inside js folder inside AWS S3 bucket to include 3 functions as follows:
    - Create 2 more functions similar to function uploadAndClassifyImage()
    - Total 3 - one for Resnet, one for Mobilenet, one for facealignment
    - Modify the function names, give corresponding Urls & also modify the button names accordingly.
    - We can take resnet url (assignment1) from S1 API pathway, mobilnet url (assignment 2) from S2 API pathway and face alignment url (assignment) from S3 API pathway we created in AWS.
11. Accordingly modify index.html inside AWS S3 bucket to accommodate 3 bodies corresponding to 3 functions we created in upload.js

<!-- FACE ALIGNMENT-->
## Face Alignment
- https://github.com/Gaju27/eva4phase2/blob/master/Session3/E4P2_Face_Alignment.ipynb

<!-- FACE SWAP -->
## Face Swamp
- https://github.com/Gaju27/eva4phase2/blob/master/Session3/E4P2S3FaceSwap_of_Trump_and_Kim.ipynb

<!-- WEBPAGE -->
## Webpage for Restful API CALL
 http://eva4p2-s3-anilbhatt1.s3-website.ap-south-1.amazonaws.com/


<!-- MARKDOWN LINKS & IMAGES -->
<!-- https://www.markdownguide.org/basic-syntax/#reference-style-links -->
[mentor-shield]: https://img.shields.io/badge/Mentor-mentor-yellowgreen
[mentor-url]: https://www.linkedin.com/in/rohanshravan/
[forks-shield]: https://img.shields.io/github/forks/othneildrew/Best-README-Template.svg?style=flat-square
[forks-url]: https://github.com/othneildrew/Best-README-Template/network/members
[stars-shield]: https://img.shields.io/github/stars/othneildrew/Best-README-Template.svg?style=flat-square
[stars-url]: https://github.com/othneildrew/Best-README-Template/stargazers
[issues-shield]: https://img.shields.io/github/issues/othneildrew/Best-README-Template.svg?style=flat-square
[issues-url]: https://github.com/othneildrew/Best-README-Template/issues
[license-shield]: https://img.shields.io/github/license/othneildrew/Best-README-Template.svg?style=flat-square
[license-url]: https://github.com/anilbhatt1/Deep_Learning_EVA4_Phase2/blob/master/LICENSE.txt
[linkedin-shield]: https://img.shields.io/badge/-LinkedIn-black.svg?style=flat-square&logo=linkedin&colorB=555


