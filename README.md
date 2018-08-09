# joint-transforms-for-torchvision

First of all, thanks [torchvision_paired_transforms](https://github.com/agaldran/torchvision_paired_transforms) a lot. This project is based on it, but there are some differences.

### Abstract
1. This project modifies ```transforms.py``` from ```torchvision 0.2.1```, in order to do the same fixed(or random) transformation on an arbitrary number of images simultaneously
1. Features:
    * Accept an arbitrary number of images as input
    * Do the same transformation on all the input. Don't distinguish them between *input image* and *target image*, just treat them the same.
    * Don't change the interface when there is only one input image. That means you don't need to change your code which once used transforms.py from torchvision.
1. Till now, these classes have been modified to accept multiple images as input
```
Compose, ToTensor, ToPILImage, Resize, CenterCrop, 
RandomCrop, RandomHorizontalFlip, RandomVerticalFlip, RandomResizedCrop, ColorJitter, RandomRotation, Grayscale, RandomGrayscale
```

### How to use
1. Change import

    Replace
    ```python
    import torchvision.transforms as transforms
    ```
    by
    ```python
    import joint_transforms_tv021 as transforms
    ```
2. Do joint transformation
    
    a. Compose
    
    ```python
        co_transforms = transforms.Compose((
            transforms.Resize(250, interpolation=Image.BILINEAR),
            transforms.RandomHorizontalFlip(),
            transforms.RandomRotation(degrees=5.0, resample=Image.BILINEAR),
            transforms.ToTensor(),
            ))
    ```
        
    b. single input image
        
        
    ```python
    input_im = co_transforms(input_im)
    ```
    or
    ```python
    input_im = transforms.ToTensor()(input_im)
    ...
    ```
        
    c. multiple input images

    ```python
    input_im, s_im, r_im, target_depth_im = co_transforms(input_im, s_im, r_im, target_depth_im)
    ```
    or
    ```python
    input_im, s_im, r_im, target_depth_im = transforms.ToTensor()(input_im, s_im, r_im, target_depth_im)
    ...
    ```

### Notification
1. Only a few transformations have already been modified till now.
1. If your input images have different channels, you'd better look for the source code to find out what joint transformations actually do, especially for some transformations aiming at changing image color, *e.g.*  Grayscale()

### Future
1. If you find any bug, please tell me.
1. If you know how to make the code seem more elegant, please tell me.
1. If you modify the remain classes, please send me a push request.
1. I hope the code can be matained until torchvision release joint transformation.




