---
layout: post
title:  "WebGL 기초 개념"
date:   2021-01-31
last_modified_at: 2021-01-31
categories: [3D]
tags: [webgl]
---

- WebGl은 웹브라우저에서 3D 그래픽을 만드는 크로스 플랫폼, 무료 API이다.
- OpenGL ES2.0을 기반으로 OpenGL shading language, GLSL 을 사용하며 그리고 많은 OpenGL API 표준을 제공한다.
- HTML5 캔버스 요소 위에서 작동하기 때문에 DOM 인터페이스와 완전히 통합된다.
- WebGL은 Firefox 4+, Google Chrome 9+, Opera 12+, Safari 5.1+, Internet Explorer 11+, Microsoft Edge build 10240+에서 사용할 수 있다. 그러나 사용자의 하드웨어도 WebGL 기능을 지원해야 한다.

<br/>

**렌더링 파이프라인**
1. vertex arrays 생성 (3차원 공간의 vertex위치, 텍스쳐, 색상, 조명...)
2. vertext buffers를 통해 GPU에 보내진다.
3. GPU는 vertex shader를 통해 vertex들을 읽는다 (vertex 위치 계산). 
4. ratsterizer는 픽셀화된 표면에 적절한 색상 그라데이션으로 조합하여 표현
5. 생성된 픽셀 사이즈 조각들은 fragment shader로 보내진다. fragment shader는 각 픽셀의 색상과 깊이를 표현하며 framebuffer에 그려진다.
6. farmebuffer는 랜더링 작업의 마지막 결과물이다. frame buffer 에는 depth buffer 및 stencil buffer가 있을 수 있으며 이는 최종 색상, 깊이 및 스텐실 값이 버퍼에 그려진다.

<br/>

**코드 연습**
```html
<canvas id="c"></canvas>    <!--canvas 요소-->
<!-- vertex, fragment shader 들을 컴파일해서 GPU에 할당해야 하는데 script 태그 안에 넣어 사용-->
<script  id="vertex-shader-2d" type="notjs">

  // an attribute will receive data from a buffer
  attribute vec4 a_position;

  // all shaders have a main function
  void main() {

    // gl_Position is a special variable a vertex shader
    // is responsible for setting
    gl_Position = a_position;
  }

</script>
<script  id="fragment-shader-2d" type="notjs">

  // fragment shaders don't have a default precision so we need
  // to pick one. mediump is a good default
  precision mediump float;

  void main() {
    // gl_FragColor is a special variable a fragment shader
    // is responsible for setting
    gl_FragColor = vec4(1, 0, 0.5, 1); // return redish-purple (rgba)
  }

</script><!--
for most samples webgl-utils only provides shader compiling/linking and
canvas resizing because why clutter the examples with code that's the same in every sample.
See https://webglfundamentals.org/webgl/lessons/webgl-boilerplate.html
and https://webglfundamentals.org/webgl/lessons/webgl-resizing-the-canvas.html
for webgl-utils, m3, m4, and webgl-lessons-ui.
-->
<script src="https://webglfundamentals.org/webgl/resources/webgl-utils.js"></script>

<script>
    /* eslint no-console:0 consistent-return:0 */
    "use strict";
    function createShader(gl, type, source) {
        var shader = gl.createShader(type);
        gl.shaderSource(shader, source);
        gl.compileShader(shader);
        var success = gl.getShaderParameter(shader, gl.COMPILE_STATUS);
        if (success) {
            return shader;
        }

        console.log(gl.getShaderInfoLog(shader));
        gl.deleteShader(shader);
    }

    function createProgram(gl, vertexShader, fragmentShader) {
        var program = gl.createProgram();
        gl.attachShader(program, vertexShader);     //두 shader를 program에 link
        gl.attachShader(program, fragmentShader);
        gl.linkProgram(program);
        var success = gl.getProgramParameter(program, gl.LINK_STATUS);
        if (success) {
            return program;
        }

        console.log(gl.getProgramInfoLog(program));
        gl.deleteProgram(program);
    }

    function main() {
        // Get A WebGL context
        var canvas = document.querySelector("#c");
        var gl = canvas.getContext("webgl");
        if (!gl) {
            return;
        }

        // Get the strings for our GLSL shaders
        var vertexShaderSource = document.querySelector("#vertex-shader-2d").text;
        var fragmentShaderSource = document.querySelector("#fragment-shader-2d").text;

        // create GLSL shaders, upload the GLSL source, compile the shaders
        var vertexShader = createShader(gl, gl.VERTEX_SHADER, vertexShaderSource);
        var fragmentShader = createShader(gl, gl.FRAGMENT_SHADER, fragmentShaderSource);

        // Link the two shaders into a program
        var program = createProgram(gl, vertexShader, fragmentShader);

        // look up where the vertex data needs to go.
        var positionAttributeLocation = gl.getAttribLocation(program, "a_position");

        // Create a buffer and put three 2d clip space points in it
        var positionBuffer = gl.createBuffer();

        // Bind it to ARRAY_BUFFER (think of it as ARRAY_BUFFER = positionBuffer)
        gl.bindBuffer(gl.ARRAY_BUFFER, positionBuffer);

        var positions = [
        0, 0,
        0, 0.5,
        0.7, 0,
        ];
        //gl.STATIC_DRAW 데이터가 많이 바뀌지 않을거라는 힌트
        gl.bufferData(gl.ARRAY_BUFFER, new Float32Array(positions), gl.STATIC_DRAW); 
                                                
        // code above this line is initialization code.
        // code below this line is rendering code.

        webglUtils.resizeCanvasToDisplaySize(gl.canvas);

        // Tell WebGL how to convert from clip space to pixels
        gl.viewport(0, 0, gl.canvas.width, gl.canvas.height);

        // Clear the canvas
        gl.clearColor(0, 0, 0, 0);
        gl.clear(gl.COLOR_BUFFER_BIT);

        // Tell it to use our program (pair of shaders)
        gl.useProgram(program);

        // Turn on the attribute
        gl.enableVertexAttribArray(positionAttributeLocation);

        // Bind the position buffer.
        gl.bindBuffer(gl.ARRAY_BUFFER, positionBuffer);

        // Tell the attribute how to get data out of positionBuffer (ARRAY_BUFFER)
        var size = 2;          // 2 components per iteration
        var type = gl.FLOAT;   // the data is 32bit floats
        var normalize = false; // don't normalize the data
        var stride = 0;        // 0 = move forward size * sizeof(type) each iteration to get the next position
        var offset = 0;        // start at the beginning of the buffer
        gl.vertexAttribPointer(
        positionAttributeLocation, size, type, normalize, stride, offset);

        // draw
        var primitiveType = gl.TRIANGLES;
        var offset = 0;
        var count = 3;
        gl.drawArrays(primitiveType, offset, count);
    }

    main();
</script>
```

출처 

[https://www.khronos.org/webgl/wiki/Getting_Started](https://www.khronos.org/webgl/wiki/Getting_Started)
[https://webglfundamentals.org/webgl/lessons/ko/webgl-fundamentals.html](https://webglfundamentals.org/webgl/lessons/ko/webgl-fundamentals.html)
[https://developer.mozilla.org/ko/docs/Web/API/WebGL_API](https://developer.mozilla.org/ko/docs/Web/API/WebGL_API)
<br/>
