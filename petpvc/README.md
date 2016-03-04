#bathomas/petpvc

This dockerfile creates a docker image that contains PETPVC (https://github.com/UCL/PETPVC) and build the executables.

###Building
```
git clone https://github.com/bathomas/docker
cd docker/petpvc
sh build.sh
```

###Example usage
The following command would apply RBV with a 6mm PSF:
```
  docker run -v </path/to/input/data>:/input \
    -v </path/to/output/data>:/output bathomas/petpvc \
    pvc_rbv /input/<pet.nii.gz> /input/<mask.nii.gz> /output/<pvcOutput.nii.gz> \
    -x 6 -y 6 -z 6
```
