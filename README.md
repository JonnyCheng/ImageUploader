# ImageUploader

A lot of awesome APIs come with HTML5,using them can help us creat a super Image Uploader.

Uploading pictures by phone is a commonplace.In order to increasing FE performance,we need to do some
pre-process for the high resolution images.Resizeing images is a normal way.

Easy way is to draw images into a small canvas.Of course,you have to keep the ratios of image and canvas 
equality.

    var width = img.width,
        height = img.height,
        cvsWidth = 1000,
        cvsHeight = 750;
    
    if(width > height){
        if(width > cvsWidth){
            height *= cvsWidth / width;
            width = cvsWidth;
        }
    }else{
        if(height > cvsHeight){
            width *= cvsHeight / height;
            height = cvsHeight;
        }
    }
    
    canvas.width = width;
    canvas.height = height;
    var ctx = canvas.getContext("2d");
    ctx.drawImage(img,0,0,width,height);
    
Put your image into a canvas,and then you can make a filter on the canvas.

    var imaData = ctx.createImageDate(width, height);
    var data = imgData.data;
    var pixls = ctx.getImageDate(0,0,width,height);
    for (var i = 0, ii = pixels.data.length; i < ii; i += 4) {
        var r = pixels.data[i + 0];
        var g =pixels.data[i + 1];
        var b = this.pixels.data[i + 2];
        data[i + 0] = (r * .393) + (g *.769) + (b * .189);
        data[i + 1] = (r * .349) + (g *.686) + (b * .168)
        data[i + 2] = (r * .272) + (g *.534) + (b * .131)
        data[i + 3] = 255;
    }
    ctx.putImageData(imgData, 0, 0);
    
Finally,you can upload the resized image.
