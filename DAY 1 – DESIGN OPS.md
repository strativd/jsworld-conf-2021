# DAY 1 – DESIGN OPS

[TOC]



## Design Systems 101

> Tech: Design systems
>
> *We hear a lot about design systems. What exactly are they? In this talk, I will introduce you to design systems defining what they are, when we should implement them and the steps to build them. We will also review some of the most popular design systems and some interesting tools and resources.*
>
> **Miriam Gonzalez** – https://miriamgonzalez.dev/
> UX/UI Frontend Developer at Neuromobile

### What is a Design System?

Design systems are a **collection of components that work together to build digital products** – *Atomic Design*

- The componenets are governed by a shared identity and best practices.
- They come with a User Manual. Think of an IKEA Manual that tells us how to use each componenet.
- A single source of truth that groups all componenets in a cohesive design.

### What problems do they solve?

- Promote a consistent experience for users and developers
- Speed up team's workflow and contribute to more development time
- More collaborative workflow
- Shared vocabulary
- Helpful documentation

### Examples

- https://github.com/alexpate/awesome-design-systems
- [Shopify – Polaris](https://polaris.shopify.com/)
- [Gitlab – Pajamas](https://design.gitlab.com/)
- [Tailwind CSS](https://tailwindcss.com/)
- [Ant Design](https://ant.design/)

### Learn more

- https://miriamgonzalez.dev/charlas/introduccion-a-sistemas-de-diseno



## Access Driven Development

> Tech: a11y, JavaScript, web accessibility
>
> *Often web accessibility is considered as an afterthought. In this session, we will explore the intricacies of a11y and learn tips and tools which will enable us to create accessible websites and applications using JavaScript.*
>
> *Key takeaways - You will learn why accessibility is important and why the development should be access focused. Also, you would learn some tips which you could start using from the very next day and contribute towards a more inclusive world.*
>
> **Anuradha Kumari**
> Development Specialist at Mediaocean

### Why care about accessibility?

*"Make resources and services usable to everyone"*

We never know the individual experience of our users so we should do our best to include everyone.

**It's not just about disabilities!**

- Technical: slow connection, smaller devices, old devices.
- Situational: like noisy environments where captions would help, for example.
- Progressive: aging user base, etc.
- *A11Y affects everyone!*

### Accessibility in Javascript

#### 1. Use semantic HTML

[`<button>` instead of `<div>` or icons](https://explore-a11y.netlify.app/button). Provides browser-based benefits out of the box. For example, makes keyboard navigation easy.

**How to create accessible buttons with divs (or any other non-semantic HTML)?**

- `tab-index`: to make the button reachable by keyboard through tab key
- `keydown event listener`: to enable triggering the button action from keyboard
- `role`: to enable acreen readers understand that it is a button
- `aria-attributes` if needed
  - For example: If the button contains only icon or image without any text, we need to add `aria-label` so that screen readers and other assistive technologies can understand what exactly does that button do. [Check demo for icon only button](https://explore-a11y.netlify.app/button#aria-demo).

```html
  <div
    tabIndex="0"
    role="button"
    id="acc-button"
    className="div-as-button"
  >
    Login
  </div>
```

```js
  const buttonEle = document.getElementById("acc-button");

  buttonEle.addEventListener("click", () => {
      // your code here on what should happen when button is clicked
    }
  );

  buttonEle.addEventListener("keydown", (event) => {
    if (event.key === ' ' || event.key === 'Enter') {
      // your code here on what should happen when button is pressed

      // prevent default so that pressing spacebar key does not scroll the content
      event.preventDefault();
    }
  });
```



#### 2. Keyboard accessibility

Navigation, click-through actions like forms, or exit componenets, [like modals](https://explore-a11y.netlify.app/modal) where focus state and context is easily lost. Focus on `tab`, `shift + tab`, `return` and `escape` keys.

A11Y MODAL: 

```html
  <section className="accessible-modal">
    <button className="open-modal-button">Click here to open modal</button>
    <button className="button-other">Some other button</button>

    <div className="modal" role="dialog" aria-modal="true">
      <div className="modal-content">
        <button className="close-modal-button" aria-label="Close modal">
          <i className="fa fa-close fa-lg" aria-hidden="true"></i>
        </button>
        <h1>Hello, the modal has opened!</h1>

        <button className="submit-modal-button">
          Submit
        </button>
      </div>
    </div>
  </section>
```

```js
  const modal = document.querySelector(".accessible-modal .modal");
  const openModalButton = document.querySelector(
    ".accessible-modal .open-modal-button"
  );
  const closeModalButton = document.querySelector(
    ".accessible-modal .close-modal-button"
  );
  const submitButton = document.querySelector(
    ".accessible-modal .submit-modal-button"
  );
  let previousActiveElement;

  const toggleModal = () => {
    modal.classList.toggle("show-modal");
  };

  const toggleModelWithFocusRestored = () => {
    toggleModal();
    previousActiveElement.focus();
  };

  const getAllFocusableElements = context =>
    Array.from(context.querySelectorAll("button"));

  const getFocusableElement = (context = "document") => {
    let focusable = getAllFocusableElements(context);
    return focusable[0];
  };

  openModalButton.addEventListener("click", () => {
    previousActiveElement = document.activeElement;
    toggleModal();
    getFocusableElement(modal).focus();
  });

  closeModalButton.addEventListener("click", () => {
    console.log("Close icon on modal clicked");
    toggleModelWithFocusRestored();
  });

  submitButton.addEventListener("click", () => {
    console.log("Submit button on modal clicked");
    toggleModelWithFocusRestored();
  });

  window.addEventListener("click", event => {
    if (event.target === modal) {
      toggleModelWithFocusRestored();
    }
  });

  // code to trap focus inside modal and close modal on ESC keypress
  let focusableElementsInModal = getAllFocusableElements(modal);
  var firstFocusableElement = focusableElementsInModal[0];
  var lastFocusableElement = focusableElementsInModal[focusableElementsInModal.length - 1];

  const handleKeyDownInModal = event => {
    // code to trap focus inside modal
    if (event.key === "Tab") {
      if (event.shiftKey) {
        if (document.activeElement === firstFocusableElement) {
          event.preventDefault();
          lastFocusableElement.focus();
        }
      } else {
        if (document.activeElement === lastFocusableElement) {
          event.preventDefault();
          firstFocusableElement.focus();
        }
      }
    } else if (event.key === "Escape") {
      // close modal on ESC keypress
      toggleModelWithFocusRestored();
    }
  };

  modal.addEventListener("keydown", handleKeyDownInModal);

```



#### 3. Event handlers

Important functionality should be managed with device-independent events.

- Use `onkeyup` instead of `onmouseup`
- Use `onkeydown` instead of `onmousedown`
- Use `onclick` instead of `onkeypress`

```js
  window.addEventListener("keydown", function (event) {
    if (event.defaultPrevented) {
      return; // Do nothing if the event was already processed
    }
  
    switch (event.key) {
      case "Down": // IE/Edge specific value
      case "ArrowDown":
        // Do something for "down arrow" key press.
        break;
      case "Up": // IE/Edge specific value
      case "ArrowUp":
        // Do something for "up arrow" key press.
        break;
      case "Left": // IE/Edge specific value
      case "ArrowLeft":
        // Do something for "left arrow" key press.
        break;
      case "Right": // IE/Edge specific value
      case "ArrowRight":
        // Do something for "right arrow" key press.
        break;
      case "Enter":
        // Do something for "enter" or "return" key press.
        break;
      case "Esc": // IE/Edge specific value
      case "Escape":
        // Do something for "esc" key press.
        break;
      default:
        return; // Quit when this doesn't handle the key event.
    }
  
    // Cancel the default action to avoid it being handled twice
    event.preventDefault();
  }, true);
```



#### 4. Announce dynamic changes

Notify users of important changes on the page. For example: view changed, notifications, error messages, form feedback.

We need to announce these changes to the users, and we can achieve it through:

- `aria-live` regions
- dedicated live region with `role="status"`, `role="log"` or `role="alert"`
- Read more about these at [MDN documentation on live regions](https://developer.mozilla.org/en-US/docs/Web/Accessibility/ARIA/ARIA_Live_Regions)

EXAMPLE FORM:

```html
<form className="announcer-form">
    <div className="submit-status" role="status" aria-live="polite"></div>
    <label>
        Enter text to announce:
        <input type="text" id="textInput" />
    </label>
    <button type="submit" id="submitTextBtn">Submit</button>
</form>
```

```js
const form = document.querySelector('form');
const liveRegion = document.querySelector('.submit-status');
const textInput = document.querySelector('#textInput');
const submitTextBtn = document.querySelector('#submitTextBtn');

const submitData = (e) => {
    e.preventDefault();
    const text = textInput.value;

    if (text.trim().length) {
        liveRegion.textContent = 'Form submitted successfully with text ' + text;
    } else {
        liveRegion.textContent = 'Error submitting form. Please enter valid text to proceed.';
    }
}

form.onsubmit = (e) => {
    e.preventDefault();
    submitData();
}
submitTextBtn.addEventListener('click', submitData)  
```



#### 5. Animations

Settings allow users to disable animations so we canot rely on them! How?

```css
/* Use CSS media query to check for animation setting */
  @media (prefers-reduced-motion: no-preference) {
    .animate-balls {
      animation: jump infinite 2s linear;
      animation-iteration-count: infinite;
    }
  }
```

```js
/* or use JS! */
  const animationClassName = matchMedia("(prefers-reduced-motion)").matches
    ? ""
    : "animate-balls";
```



### Testing for A11y

https://explore-a11y.netlify.app/testing

1. Unplug your mouse
2. Use a screenreader
3. [Use tools, extensions to audit](https://explore-a11y.netlify.app/testing)
4. Consult real users!

### Learn more

- [tota11y](https://khan.github.io/tota11y/) an accessibility visualization toolkit
- https://www.webaccessibility.com/
- [A11y example components](https://explore-a11y.netlify.app/button): button, modal, events, titles, animations, dark mode, carousels.



## Third piece of the Frontend Pie: CSS

> Tech: CSS, Sass, SCSS
>
> *It just needs a quick look at the Frontend trends to realize that recently the spotlight is on the JavaScript and all of its frameworks, But the Frontend pie has three pieces (HTML, CSS & JS). Without the other pieces, you cannot have a complete pie.*
>
> **Negar Jamalifard**
> Creator at Loudly GmbH

**JavaScript alone is not enough to be a good frontend developer!**

- CSS is performant and powerful! We shouldn't default to Javascript.
- Default to CSS animations whenever possible! Javascript animations consume browser resources that don't need to be used with CSS. 
- CSS has way better error handling than JS! It just ignores code it doesn't know.

### Selectors

CSS provides powerful selectors to perform complex and performant logic on our HTML. Know the selectors available to you:

- https://www.freecodecamp.org/news/css-selectors-cheat-sheet/
- https://www.w3schools.com/cssref/css_selectors.asp

**Specificity**: different selectors have different specificity which controls which wins when there are several selectors which could apply to one element.

**Cascades**: if specificity is the same then we'll use the styles from the previous specificity.

### [How to learn CSS](https://www.smashingmagazine.com/2019/01/how-to-learn-css/)

***Play!*** Use Codepen to rebuild your favourite memes, logos or designs :)



## Encoding Emojis 🤓

> Tech: i18n, [Emoji Encoding](https://dev.to/naeohmi/emoji-encoding-unicode-and-internationalization-with-naomi-meyer-34d3), � Unicode, & Internationalization
>
> *Have you ever wondered how emoji and complex scripting languages are encoded to work correctly across browsers and devices - for billions of people around the world?*
>
> **Naomi Meyer**
> Software Development Engineer at Adobe

### Wait, why does `'👩🏿‍🎤'.length = 7` ?

**TLDR** every character is ultimately represented in binary – ones and zeros – using character encoding [but emojis need more than one character to live in memory...](https://dev.to/naeohmi/emoji-encoding-unicode-and-internationalization-with-naomi-meyer-34d3)



### Encoding

> The character encoding is what transforms abstract code points into physical bits: code units.

- Standardizes the digital representation of human readable characters.
- The basic building blocks of software!

| ASCII CHAR | BINARY   | UNICODE | HEX  |
| ---------- | -------- | ------- | ---- |
| **y**      | 01111001 | U+0079  | 79   |
| **z**      | 01111010 | U+007A  | 7A   |
| **{**      | 01111011 | U+007B  | 7B   |
| **\|**     | 01111100 | U+007C  | 7C   |
| **}**      | 01111101 | U+007D  | 7D   |
| **~**      | 01111110 | U+007E  | 7E   |



### ASCII... 👾

- "American Standard Code for Information Interchange" in the 1960s.
- 7 bits (7 ones and zeros) can represent 128 standard characters, maximum.



### � W � T � F �

- With only 7 bits you can't represent most characters around the globe
- So what about `ñ ú ä ç Ł ö æ` . . .



### Unicode! 🎮

With the World Wide Web there was a need for a **more inclusive standard**.

Important for accessibility – a11y, globalization – i18n, and technological progress!

- 1991: Unicode v1
- 2020: Unicode v13 🥳

**Code point**: "a number assigned to a single abstract character"

- For example, `U+0041 = A` where `U` means Unicode and `0041` – must be a hexidecimal character – represents the latin letter "A"
- This is the birth of Unicode version one.



### Unicode Planes ✈️ 

| **"BASIC MULTILINGUAL PLANE"** 🌎 | **CODE POINTS**         |
| -------------------------------- | ----------------------- |
| Plane 0                          | **U+0**000 ➡ U+FFFF     |
| **"ASTRAL PLANES"** 🪐            |                         |
| Plane 1                          | **U+1**0000 ➡ U+1FFFF   |
| Plane 2                          | **U+2**0000 ➡ U+2FFFF   |
| . . .                            |                         |
| Plane 15                         | **U+F**0000 ➡ U+FFFFF   |
| Plane 16                         | **U+10**0000 ➡ U+10FFFF |



### Unicode Transformation Format (UTF)

```html
<head>
  <meta charset="UTF-8"> <!-- 🤔 -->
</head>
```

Determines how much information (bits) is required to build the page!

| CHARACTER | UTF ENCODING | BITS                                |
| --------- | ------------ | ----------------------------------- |
| A         | UTF-8        | 01000001                            |
| A         | UTF-16       | 00000000 01000001                   |
| A         | UTF-32       | 00000000 00000000 00000000 01000001 |
| あ        | UTF-8        | 11100011 10000001 10000010          |
| あ        | UTF-16       | 00110000 01000010                   |
| あ        | UTF-32       | 00000000 00000000 00110000 01000010 |



### JavaScript

**ECMAScript**, the standardized version of JavaScript, defines how characters should be interpreted as either UCS-2 or UTF-16

- **UCS-2**: 2-byte Universal Character Set
- **UTF-16**: 16-bit Unicode Transformation Format



```javascript
const string = 'å';
console.log(string.length)  //==> 2 ... ಠ_ಠ
```

**å = "atomic grapheme" is actually two unicode characters!** 🤯

1. `U+0061` – latin small letter a (rendered as a)
2. `U+030A` – combining ring above (rendered as ◌̊)



```javascript
const string = 'cafe\u0301s';

console.log(string) //==> 'cafés'
console.log(string.length)  //==> 6
console.log(string.split(''))  //==> ['c', 'a', 'f', 'e', '´', 's']

console.log(string.split('').reverse().join('')) //==> `śefac`
// ... say fac, indeed! ಠ_ಠ
```

[String.prototype.normalize()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/normalize)

> The **`normalize()`** method returns the Unicode Normalization Form of the string.

```js
const string = 'cafe\u0301s';

console.log(string.normalize()) //==> 'cafés'
console.log(string.normalize().length)  //==> 5
console.log(string.normalize().split(''))  //==> ['c', 'a', 'f', 'é', 's']
```



**💩 Pile of Poo Test 💩**

Given all this Uni-chaos... Test your JavaScript functions, HTML forms, and regex validations, using the "pile of poo test":

`💩Iñtërnâtiônàlizætiøn☃💩`



### Emojis 🥳

```js
Array.from("💩").length === 1; //==> woo! (╯°o°)╯

Array.from("❤️").length === 2; //==> wtf! ಠ_ಠ
```

Emojis require extra characters to be stored in memory!

❤️ = `U+2764` ("heavy black heart" – ❤) plus `U+FE0F` ("variantion selector-16") pluuuus...

**The "zwidge" (ZWJ)** 📌

- [Zero Width Joiner](https://emojipedia.org/zero-width-joiner/) is a Unicode character that joins two or more other characters together in sequence to create a new character/emoji!
- `U+200D` 

**Emoji = Astral Code Points**

> An astral code point requires two code units: a surrogate pair. As you saw in the previous example – `e` and  `´` – to encode `U+1F600` (`😀`) in UTF-16 a surrogate pair is used: `0xD83D 0xDE00`.

😀 = `U+1F600`

- 5 Hexidecimal digits requires 21 bits to save in memory...
- With JavaScript (UTF-16 or 16 bits) that requires two code units!

```js
function getSurrogatePair(astralCodePoint) {
  let highSurrogate = 
     Math.floor((astralCodePoint - 0x10000) / 0x400) + 0xD800;
  let lowSurrogate = (astralCodePoint - 0x10000) % 0x400 + 0xDC00;
  return [highSurrogate, lowSurrogate];
}

getSurrogatePair(0x1F600); // => [0xDC00, 0xDFFF]

function getAstralCodePoint(highSurrogate, lowSurrogate) {
  return (highSurrogate - 0xD800) * 0x400 
      + lowSurrogate - 0xDC00 + 0x10000;
}

getAstralCodePoint(0xD83D, 0xDE00); // => 0x1F600
```



### Soooo why does `'👩🏿‍🎤'.length = 7` ?

**👩 - U+1F469 - 2**

**🏿 - U+1F3FF - 2**

- **U+200D - 1** (the "zwidge")

**🎤 - U+1F3A4 - 2**

**`'👩🏿‍🎤'.length = 7`**

🎉 🎉 🎉

