---
layout: post
title:  "WebGL - GLSL/Shader(4)"
date:   2021-02-04
last_modified_at: 2021-02-04
categories: [3D]
tags: [webgl]
---

**patterns**
패턴의 반복
```javascript
#ifdef GL_ES
precision mediump float;
#endif

uniform vec2 u_resolution;
uniform float u_time;

float circle(in vec2 _st, in float _radius){
    vec2 l = _st-vec2(0.5);
    return 1.-smoothstep(_radius-(_radius*0.01),
                         _radius+(_radius*0.01),
                         dot(l,l)*4.0);
}

void main() {
	vec2 st = gl_FragCoord.xy/u_resolution;
    vec3 color = vec3(0.0);

    st *= 3.0;      // Scale up the space by 3
    st = fract(st); // Wrap around 1.0

    // Now we have 9 spaces that go from 0-1

    color = vec3(st,0.0);
    //color = vec3(circle(st,0.5));

	gl_FragColor = vec4(color,1.0);
}
```

<br/>

**Random**
```javascript
#ifdef GL_ES
precision mediump float;
#endif

uniform vec2 u_resolution;
uniform vec2 u_mouse;
uniform float u_time;

float random (vec2 st) {
    return fract(sin(dot(st.xy,
                         vec2(12.9898,78.233)))*
        43758.5453123);
}

void main() {
    vec2 st = gl_FragCoord.xy/u_resolution.xy;

    float rnd = random( st );

    gl_FragColor = vec4(vec3(rnd),1.0);
}
```

<br/>

**Noise**

Random과 비슷하게 불특정 값을 표현하지만 주변값들이 비슷한 흐름을 갖는다.

```javascript
#ifdef GL_ES
precision mediump float;
#endif

uniform vec2 u_resolution;
uniform vec2 u_mouse;
uniform float u_time;

float random (float val) {
   return fract(sin(f*654.876)*915.876);
}

float noise (float val) {
    float i = floor(val);
    float f = fract(val);
    
    float ret;
    ret = mix(random(i), random(i+1.), f);
    f = f*f*f*(f*(f*6.-15.)+10.);
    ret = mix(random(i), random(i+1.), f);
    return ret;
}

void main() {
    vec2 coord = gl_FragCoord.xy/u_resolution.xy;
    coord.x *= u_resolution.x/u_resolution.y;
    
    vec3 col = vec3(noise(coord.x*10.));

    gl_FragColor = vec4(col, 1.0);
}
```

출처 

[https://learnopengl.com/Getting-started/Coordinate-Systems](https://learnopengl.com/Getting-started/Coordinate-Systems)
[https://thebookofshaders.com/](https://thebookofshaders.com/)
[https://opentutorials.org/module/3659/21954](https://opentutorials.org/module/3659/21954)
<br/>
