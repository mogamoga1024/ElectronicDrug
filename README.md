# ElectronicDrug
お手軽電子ドラッグ

以下をブラウザのコンソールに貼り付けて実行

```js
function getAllElements(currentWindow = window) {
    let elements = [];
    try {
        elements = [...currentWindow.document.querySelectorAll("*")];
        const iframes = currentWindow.document.querySelectorAll("iframe");
        for (const iframe of iframes) {
            elements = elements.concat(getAllElements(iframe.contentWindow));
        }
    }
    catch (e) {
        // DOMException: Blocked a frame with origin XXX from accessing a cross-origin frame.
        console.error(e);
    }
    return elements;
}

const elements = getAllElements();
elements.forEach((element) => {
    const hue = Math.floor(Math.random() * 360);
    element.style.backgroundColor = `hsl(${hue} 100% 50%)`;
    element.style.color = `hsl(${hue + 180} 100% 50%)`;
});

const body = document.querySelector("body");
let hue = 0;
body.style.filter = `invert(100%) hue-rotate(${hue}deg)`;

// 色がうにょうにょ変化します。気持ち悪くなるかもしれないので実行する際は部屋を明るくして離れてみてください。
setInterval(function() {
    hue = (hue + 1) % 360;
    body.style.filter = `invert(100%) hue-rotate(${hue}deg)`;
}, 1);
```
