# Image-Carousel
## AIM
To develop an Image Carousel in react using hooks.
## ALGORITHM
1. Create a react project using npx-create-react-app project name 
2. Create the required components for carousel like slidercontent.js, slider.js, arrows.js and dots.js
3. Import the required images from internet for the slides.
4. Include those images in the components using import command.
5. Create a .css file for the carousel outlook.
6. Launch the program using npm start
7. End the program. 

## PROGRAM
### imageslider.js
```
import First from "../assets/img1.jpeg";
import Second from "../assets/img2.jpg";
import Third from "../assets/img5.jpeg";
import Fourth from "../assets/img6.jpeg";

export default [
  {
    title: "First Slide",
    description: "This is the first slider Image of our carousel",
    urls: First,
  },
  {
    title: "Second Slide",
    description: "This is the second slider Image of our carousel",
    urls: Second,
  },
  {
    title: "Third Slide",
    description: "This is the Third slider Image of our carousel",
    urls: Third,
  },
  {
    title: "Fourth Slide",
    description: "This is the Fourth slider Image of our carousel",
    urls: Fourth
  },
  
];
```
### slidercontent.js
```
import React from "react";

function SliderContent({ activeIndex, sliderImage }) {
  return (
    <section>
      {sliderImage.map((slide, index) => (
        <div
          key={index}
          className={index === activeIndex ? "slides active" : "inactive"}
        >
          <img className="slide-image" src={slide.urls} alt="" />
          <h2 className="slide-title">{slide.title}</h2>
          <h3 className="slide-text">{slide.description}</h3>
        </div>
      ))}
    </section>
  );
}

export default SliderContent;
```
### slider.js
```
import React, { useEffect, useState } from "react";
import SliderContent from "./slidercontent";
import Dots from "./dots";
import Arrows from "./arrows";
import sliderImage from "./imageslider";
import "./slider.css";

const len = sliderImage.length - 1;

function Slider(props) {
  const [activeIndex, setActiveIndex] = useState(0);

  useEffect(() => {
    const interval = setInterval(() => {
      setActiveIndex(activeIndex === len ? 0 : activeIndex + 1);
    }, 5000);
    return () => clearInterval(interval);
  }, [activeIndex]);

  return (
    <div className="slider-container">
      <SliderContent activeIndex={activeIndex} sliderImage={sliderImage} />
      <Arrows
        prevSlide={() =>
          setActiveIndex(activeIndex < 1 ? len : activeIndex - 1)
        }
        nextSlide={() =>
          setActiveIndex(activeIndex === len ? 0 : activeIndex + 1)
        }
      />
      <Dots
        activeIndex={activeIndex}
        sliderImage={sliderImage}
        onclick={(activeIndex) => setActiveIndex(activeIndex)}
      />
    </div>
  );
}

export default Slider;
```
### dots.js
```
import React from "react";

function Dots({ activeIndex, onclick, sliderImage }) {
  return (
    <div className="all-dots">
      {sliderImage.map((slide, index) => (
        <span
          key={index}
          className={`${activeIndex === index ? "dot active-dot" : "dot"}`}
          onClick={() => onclick(index)}
        ></span>
      ))}
    </div>
  );
}

export default Dots;
```
### arrows.js
```
import React from "react";

function Arrows({ prevSlide, nextSlide }) {
  return (
    <div className="arrows">
      <span className="prev" onClick={prevSlide}>
        &#10094;
      </span>
      <span className="next" onClick={nextSlide}>
        &#10095;
      </span>
    </div>
  );
}

export default Arrows;

```
### slider.css
```
* {
    box-sizing: border-box;
    margin: 0;
  }
  
  :root {
    --heights: 50vh;
    --widths: 100%;
  }
  
  .slider-container {
    height: var(--heights);
    width: var(--widths);
    position: relative;
    margin: auto;
    overflow: hidden;
  }
  
  .active {
    display: inline-block;
  }
  
  .inactive {
    display: none;
  }
  
  .slides {
    height: var(--heights);
    width: var(--widths);
    position: relative;
  }
  
  .slide-image {
    width: 100%;
    height: 100%;
    position: absolute;
    object-fit: cover;
  }
  
  .slide-title,
  .slide-text {
    width: 100%;
    height: 100%;
    color: white;
    font-size: 50px;
    position: absolute;
    text-align: center;
    top: 40%;
    z-index: 10;
  }
  
  .slide-text {
    top: 65%;
    font-size: 2rem;
  }
  
  .prev,
  .next {
    color: transparent;
    cursor: pointer;
    z-index: 100;
    position: absolute;
    top: 50%;
    width: auto;
    padding: 1rem;
    margin-top: -3rem;
    font-size: 40px;
    font-weight: bold;
    border-radius: 0px 5px 5px 0px;
  }
  
  .slider-container:hover .prev,.slider-container:hover .next {
    color: black
  }
  
  .slider-container:hover .prev:hover,
  .slider-container:hover .next:hover {
    color: white;
    background-color: rgba(0, 0, 0, 0.6);
    transition: all 0.5s ease-in;
  }
  
  .next {
    right: 0;
    border-radius: 5px 0px 0px 5px;
  }
  
  .all-dots {
    width: 100%;
    height: 100%;
    position: absolute;
    display: flex;
    top: 85%;
    justify-content: center;
    z-index: 200;
  }
  
  .dot {
    cursor: pointer;
    height: 1.5rem;
    width: 1.5rem;
    margin: 0px 3px;
    background-color: transparent;
    /* background-color: rgba(0, 0, 0, 0.3); */
    border-radius: 50%;
    display: inline-block;
  }
  
  .slider-container:hover .dot:hover {
    background-color: rgba(255, 255, 255, 0.5);
  }
  
  /* .active-dot {
    background-color: rgba(255, 255, 255, 0.5);
  } */
  
  .slider-container:hover .dot{
    background-color: rgba(0, 0, 0, 0.3);
  }
  .slider-container:hover .active-dot{
    background-color: rgba(255, 255, 255, 0.5);
  }
  
  .play-pause {
    color: black;
  }
```
### App.js
```
import Slider from "./components/slider";
function App() {
  return <Slider />;
}
export default App;
```
## OUTPUT

<img width="960" alt="image" src="https://github.com/Shavedha/Image-Carousel/assets/93427376/989da404-a8c8-4e0f-829e-118d60d8dd11">
<img width="960" alt="image" src="https://github.com/Shavedha/Image-Carousel/assets/93427376/933ac2ce-0ef7-4b2f-ab96-f718bb97475e">
<img width="960" alt="image" src="https://github.com/Shavedha/Image-Carousel/assets/93427376/1f599cf1-59f6-4645-9a45-bf6866042ea7">
<img width="960" alt="image" src="https://github.com/Shavedha/Image-Carousel/assets/93427376/54cbad2b-5601-4eee-8939-6471eda4c37c">

## RESULT
Thus an Carousel application using react is created successfully.
