---
layout: post
title:  "GLSL/Shader(2)"
date:   2021-02-02
last_modified_at: 2021-02-02
categories: [GLSL]
tags: [GLSL]
---

**colors**

개별요소 접근

```javascript
vec4 vector;
vector[0] = vector.r = vector.x = vector.s;
vector[1] = vector.g = vector.y = vector.t;
vector[2] = vector.b = vector.z = vector.p;
vector[3] = vector.a = vector.w = vector.q;
```

mix(r 값, b 값, g값의 혼합)
```javascript
#ifdef GL_ES
precision mediump float;
#endif

#define PI 3.14159265359

uniform vec2 u_resolution;
uniform vec2 u_mouse;
uniform float u_time;

vec3 colorA = vec3(0.149,0.141,0.912);
vec3 colorB = vec3(1.000,0.833,0.224);

float plot (vec2 st, float pct){
  return  smoothstep( pct-0.01, pct, st.y) -
          smoothstep( pct, pct+0.01, st.y);
}

void main() {
    vec2 st = gl_FragCoord.xy/u_resolution.xy;
    vec3 color = vec3(0.0);

    vec3 pct = vec3(st.x);

    // pct.r = smoothstep(0.0,1.0, st.x);
    // pct.g = sin(st.x*PI);
    // pct.b = pow(st.x,0.5);

    color = mix(colorA, colorB, pct);

    // Plot transition lines for each channel
    color = mix(color,vec3(1.0,0.0,0.0),plot(st,pct.r));
    color = mix(color,vec3(0.0,1.0,0.0),plot(st,pct.g));
    color = mix(color,vec3(0.0,0.0,1.0),plot(st,pct.b));

    gl_FragColor = vec4(color,1.0);
}
```
<br/>

**atan**
- Return the arc-tangent of the parameters

<br/>

**qualifier**

- in (default) 깊은 복사
- out default로 initialize
- inout reference 복사

<br/>

**Shaping Function**

- rectangle

```javascript
vec3 rect(vec2 coord, vec2 loc, vec2 size){
    vec2 sw = loc -size/2.;
    vec2 ne = loc+size/2.;
    vec2 pct = step(sw, coord);
    pct -= step(ne, coord);
    return vec3(pct.x * pct.y);

}

void main() {
    vec2 coord = gl_FragCoord.xy/u_resolution;
    vec3 col = rect(coord, vec2(.5), vec2(.5));
    gl_FragColor = vec4(col, 1.);
}
```

- circle

```javascript
vec3 circle(vec2 coord, vec2 loc, float r){

    float d;
    d = length(coord - loc);
    d = smoothstep(r, r+0.01, d);
    return vec3(d);    
}

void main() {
    vec2 coord = gl_FragCoord.xy/u_resolution;
    vec3 col = circle(coord, vec2(.5), .3);
    gl_FragColor = vec4(col, 1.);
}
```

- circle2

```javascript
void main() {
    vec2 coord = gl_FragCoord.xy/u_resolution;
    coord.x *= u_resolution.x/u_resolution.y;
    
    coord = coord*2. - 1.;
    
    vec2 point = vec2(.3);
    
    float d = distance(abs(coord), point);
    d = mod(d*10., 1.);
    vec3 col = vec3(d);
    
    gl_FragCoord = vec4(col, 1.);
}
```

- circle3

```javascript
void main() {
    vec2 coord = gl_FragCoord.xy/u_resolution;
    coord = coord*2. - 1.;
    coord.x *= u_resolution.x/u_resolution.y;

    float a = atan(coord.y, coord.x);
    float d = length(coord);

    a += 0.;
    a *= 3.;
    
    float r = sin(a);
    vec3 col = vec3(step(r, d));
    
    gl_FragCoord = vec4(col, 1.);
}
```

<br/>

출처 

[https://thebookofshaders.com/](https://thebookofshaders.com/)
[https://opentutorials.org/module/3659/21954](https://opentutorials.org/module/3659/21954)
<br/>
