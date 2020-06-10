# group_06

[![pipeline status](https://git.chalmers.se/courses/dit638/students/group_06/badges/master/pipeline.svg)](https://git.chalmers.se/courses/dit638/students/group_06/commits/master)

## How to clone and install
In order to be able to clone the repository, an SSH key is necessary. The steps to clone and install are:
   1. Navigate to your .ssh folder in the root directory.
   2. Run ssh-keygen with the preferred encryption type (RSA / ED25519).
   3. Copy your public key that has been generated and paste it into Gitlab under Your SSH Keys.
   4. Navigate into a folder where you intend to clone the repository. Do: <br>
        *$ git clone git@git.chalmers.se:courses/dit638/students/group_06.git*
    <br>
   5. Configure your Git authentication using <br>
        *$ git config user.email " ... "* <br>
    and <br>
        *$ git config user.name " ... "*   
    <br>
   6. To run the program, navigate into the sourse_code folder and run the command:
        <br>
        *$ docker run --rm --init --net=host --name=opendlv-vehicle-view -v $PWD:/opt/vehicle-view/recordings -v /var/run/docker.sock:/var/run/docker.sock -p 8081:8081 chalmersrevere/opendlv-vehicle-view-multi:v0.0.60*
        <br>
        From there, you can go to
        <br>
        http://localhost:8081/
        <br>
        And click on the folder to select a video clip to be analyzed. 
        <br>     
    7.Open a new terminal window in the same directory and run the command:
        <br>
        *$ docker build https://github.com/chalmers-revere/opendlv-video-h264-decoder.git#v0.0.3 -f Dockerfile.amd64 -t h264decoder:v0.0.3*
        To download the h264Decoder if you don't have it on your machine, followed by:
        <br>
        *$ xhost +*
        <br>
        In order to allow access to the shared memory. Followed by: 
        <br>
        *$ docker run --rm -ti --net=host --ipc=host -e DISPLAY=$DISPLAY -v /tmp:/tmp h264decoder:v0.0.3 --cid=253 --name=img*
        <br>
        To start the h264Decoder
        <br>
    8. Open a new terminal window in the same directory and run the commands:
        <br>
    *$ docker build -f Dockerfile -t my-opencv-example .*
        <br>
        then run: 
    <br>
    *$ docker run --rm -ti --net=host --ipc=host -e DISPLAY=$DISPLAY -v /tmp:/tmp my-opencv-example:latest --cid=253 --name=img --width=640 --height=480 --verbose*
        <br>
    To start the microservice

## Working conventions and policies
   1. Features should be added only upon group discussions and agreement to improve the system.
   2. Features should be present in the working Gitlab boards.
   3. Features should be broken down into tasks - tasks can be taken on by one or multiple interested members.
   4. Tasks can be worked on individually, but another member can join in to work together (to achieve pair programming).
   5. Depending on the importance of the feature and how early it was implemented, some solutions include: reverting to a previous working version, waiting before merging a feature branch into the master branch in order to assess if the feature can be integrated, or using different branches for ideas that might not be feasible to avoid clumping the master branch.
   6. Commit messages should include a label in the beginning of the message (feature, bugfix, etc.).
   7. Commit messages should be self-explanatory, directly naming what the commit does to the product.
   8. Commits should have a label, a title and a description (for extra details that might not be necessary in the title).
   9. Commit title should not contain more than 10 words.
   10. Commit titles should start with a verb ('added', 'created', 'removed', etc.), followed by the rest of the sentence.

## References: 
Noise cancellation: 

1.  https://docs.opencv.org/2.4/doc/tutorials/imgproc/opening_closing_hats/opening_closing_hats.html 
2.  https://docs.opencv.org/2.4/doc/tutorials/imgproc/erosion_dilatation/erosion_dilatation.html 
3.  https://docs.opencv.org/2.4/doc/tutorials/imgproc/gausian_median_blur_bilateral_filter/gausian_median_blur_bilateral_filter.html 

Contouring: 

1.  https://docs.opencv.org/2.4/doc/tutorials/imgproc/shapedescriptors/bounding_rects_circles/bounding_rects_circles.html?fbclid=IwAR0-pDNlG6-RUKefCiZCFOZjUkz0GT58vEKnBcEX_ImxaShLet0RKX_HMM4
2.  https://www.learnopencv.com/find-center-of-blob-centroid-using-opencv-cpp-python/

White Pixels: 

1.  https://stackoverflow.com/questions/16929190/fastest-way-to-get-number-of-white-pixels-in-a-binary-image-using-opencv

Warp Images:

1.  http://opencvexamples.blogspot.com/2014/01/perspective-transform.html
2.  https://chatbotslife.com/self-driving-cars-advanced-computer-vision-with-opencv-finding-lane-lines-488a411b2c3d
3.  https://docs.opencv.org/2.4/modules/core/doc/drawing_functions.html