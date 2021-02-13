---
layout: post
title:  "WebGL - 이미지 처리"
date:   2021-02-06
last_modified_at: 2021-02-06
categories: [WEBGL]
tags: [WEBGL]
---

fragment shader를 사용해서 각 픽섹을 그릴 때 vertex shader에 제공한 값을 보간한다.

```html
<script id="fragment-shader-2d" type="x-shader/x-fragment">
precision mediump float;
//texture
uniform sampler2D u_image;
//vertex sahder에서 전달된 texCoords
varying vec2 v_texCoord;

void main() {
    // texture의 색상 탐색
    gl_FragColor = texture2D(u_image, v_texCoord);
}
</script>
```
```javascript
function main() {
    var image = new Image();
    image.src = "http://someimage/on/our/server";
    image.onload = function() {
        render(image);
    }
}

function render(image) {
    var canvas = document.querySelector("#canvas");
    var gl = canvas.getContext("webgl");
    if (!gl) {
       return;
    }

    var program = webglUtils.createProgramFromScripts(gl, ["vertex-shader-2d", "fragment-shader-2d"]);
    
    var positionLocation = gl.getAttribLocation(program, "a_position");
    var texcoordLocation = gl.getAttribLocation(program, "a_texCoord");

    var positionBuffer = gl.createBuffer();
    gl.bindBuffer(gl.ARRAY_BUFFER, positionBuffer);
    setRectangle(gl, 0, 0, image.width, image.height);
    gl.bufferData(gl.ARRAY_BUFFER, new Float32Array([
        0.0, 0.0,
        1.0, 0.0,
        0.0, 1.0,
        0.0, 1.0,
        1.0, 0.0,
        1.0, 1.0,
    ]), gl.STATIC_DRAW);

    var texture = gl.createTexture();
    gl.bindTexture(gl.TEXTURE_2D, texture);

    gl.texParameteri(gl.TEXTURE_2D, gl.TEXTURE_WRAP_S, gl.CLAMP_TO_EDGE);
    gl.texParameteri(gl.TEXTURE_2D, gl.TEXTURE_WRAP_T, gl.CLAMP_TO_EDGE);
    gl.texParameteri(gl.TEXTURE_2D, gl.TEXTURE_MIN_FILTER, gl.NEAREST);
    gl.texParameteri(gl.TEXTURE_2D, gl.TEXTURE_MAG_FILTER, gl.NEAREST);

    gl.texImage2D(gl.TEXTURE_2D, 0, gl.RGBA, gl.RGBA, gl.UNSIGNED_BYTE, image);

    var resolutionLocation = gl.getUniformLocation(program, "u_resolution");
    
    webglUtils.resizeCanvasToDisplaySize(gl.canvas);

    gl.viewport(0, 0, gl.canvas.width, gl.canvas.height);

    gl.clearColor(0, 0, 0, 0);
    gl.clear(gl.COLOR_BUFFER_BIT);

     gl.useProgram(program);
    
      // Turn on the position attribute
      gl.enableVertexAttribArray(positionLocation);
    
      // Bind the position buffer.
      gl.bindBuffer(gl.ARRAY_BUFFER, positionBuffer);
    
      // Tell the position attribute how to get data out of positionBuffer (ARRAY_BUFFER)
      var size = 2;          // 2 components per iteration
      var type = gl.FLOAT;   // the data is 32bit floats
      var normalize = false; // don't normalize the data
      var stride = 0;        // 0 = move forward size * sizeof(type) each iteration to get the next position
      var offset = 0;        // start at the beginning of the buffer
      gl.vertexAttribPointer(
          positionLocation, size, type, normalize, stride, offset);
    
      // Turn on the texcoord attribute
      gl.enableVertexAttribArray(texcoordLocation);
    
      // bind the texcoord buffer.
      gl.bindBuffer(gl.ARRAY_BUFFER, texcoordBuffer);
    
      // Tell the texcoord attribute how to get data out of texcoordBuffer (ARRAY_BUFFER)
      var size = 2;          // 2 components per iteration
      var type = gl.FLOAT;   // the data is 32bit floats
      var normalize = false; // don't normalize the data
      var stride = 0;        // 0 = move forward size * sizeof(type) each iteration to get the next position
      var offset = 0;        // start at the beginning of the buffer
      gl.vertexAttribPointer(
          texcoordLocation, size, type, normalize, stride, offset);
    
      // set the resolution
      gl.uniform2f(resolutionLocation, gl.canvas.width, gl.canvas.height);
    
      // Draw the rectangle.
      var primitiveType = gl.TRIANGLES;
      var offset = 0;
      var count = 6;
      gl.drawArrays(primitiveType, offset, count);
}

function setRectangle(gl, x, y, width, height) {
  var x1 = x;
  var x2 = x + width;
  var y1 = y;
  var y2 = y + height;
  gl.bufferData(gl.ARRAY_BUFFER, new Float32Array([
     x1, y1,
     x2, y1,
     x1, y2,
     x1, y2,
     x2, y1,
     x2, y2,
  ]), gl.STATIC_DRAW);
}
```

출처 

[https://webglfundamentals.org/webgl/lessons/ko/webgl-image-processing.html](https://webglfundamentals.org/webgl/lessons/ko/webgl-image-processing.html)
<br/>
