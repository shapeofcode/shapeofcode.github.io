---
layout: post
title:  "WebGL - GLSL/Shader(3)"
date:   2021-02-03
last_modified_at: 2021-02-03
categories: [3D]
tags: [webgl]
---

**Matrices**

5개의 좌표 시스템을 거쳐 버텍스들이 표현된다. 

- LOCAL SPACE : 오브젝트 자체의 좌표들이다.
- WORLD SPACE : 다른 오브젝트들과의 상관 관계를 갖는 좌표들이다.
- VIEW SPACE : WORLD SPACE 좌표를 카메라 또는 보는 시점에 따라 변환한 좌표들이다.
- CLIP SPACE : -1.0 과 1.0 사이 범위의 클립 좌표에 투영하여 원근을 추가할 수 있다.
- SCREEN SPACE : glViewport에서 정의된 -1.0 과 1.0 사이의 좌표들이 화면 좌표계로 표현된다.

**Translate**
```javascript
#ifdef GL_ES
precision mediump float;
#endif

uniform vec2 u_resolution;
uniform float u_time;

float box(in vec2 _st, in vec2 _size){
    _size = vec2(0.5) - _size*0.5;
    vec2 uv = smoothstep(_size,
                        _size+vec2(0.001),
                        _st);
    uv *= smoothstep(_size,
                    _size+vec2(0.001),
                    vec2(1.0)-_st);
    return uv.x*uv.y;
}

float cross(in vec2 _st, float _size){
    return  box(_st, vec2(_size,_size/4.)) +
            box(_st, vec2(_size/4.,_size));
}

void main(){
    vec2 st = gl_FragCoord.xy/u_resolution.xy;
    vec3 color = vec3(0.0);

    // To move the cross we move the space
    vec2 translate = vec2(cos(u_time),sin(u_time));
    st += translate*0.35;

    // Show the coordinates of the space on the background
    // color = vec3(st.x,st.y,0.0);

    // Add the shape on the foreground
    color += vec3(cross(st,0.25));

    gl_FragColor = vec4(color,1.0);
}
```
**Rotation**
```javascript
#ifdef GL_ES
precision mediump float;
#endif

#define PI 3.14159265359

uniform vec2 u_resolution;
uniform float u_time;

mat2 rotate2d(float _angle){
    return mat2(cos(_angle),-sin(_angle),
                sin(_angle),cos(_angle));
}

float box(in vec2 _st, in vec2 _size){
    _size = vec2(0.5) - _size*0.5;
    vec2 uv = smoothstep(_size,
                        _size+vec2(0.001),
                        _st);
    uv *= smoothstep(_size,
                    _size+vec2(0.001),
                    vec2(1.0)-_st);
    return uv.x*uv.y;
}

float cross(in vec2 _st, float _size){
    return  box(_st, vec2(_size,_size/4.)) +
            box(_st, vec2(_size/4.,_size));
}

void main(){
    vec2 st = gl_FragCoord.xy/u_resolution.xy;
    vec3 color = vec3(0.0);

    // move space from the center to the vec2(0.0)
    st -= vec2(0.5);
    // rotate the space
    st = rotate2d( sin(u_time)*PI ) * st;
    // move it back to the original place
    st += vec2(0.5);

    // Show the coordinates of the space on the background
    // color = vec3(st.x,st.y,0.0);

    // Add the shape on the foreground
    color += vec3(cross(st,0.4));

    gl_FragColor = vec4(color,1.0);
}
```

<br/>

회전변환식 유도
![회전변환식 유도](../../../assets/images/rotate2d.jpg)

<br/>

출처 

[https://blog.naver.com/dalsapcho/20144939371](https://blog.naver.com/dalsapcho/20144939371)
[https://learnopengl.com/Getting-started/Coordinate-Systems](https://learnopengl.com/Getting-started/Coordinate-Systems)
[https://thebookofshaders.com/](https://thebookofshaders.com/)
[https://opentutorials.org/module/3659/21954](https://opentutorials.org/module/3659/21954)
<br/>
