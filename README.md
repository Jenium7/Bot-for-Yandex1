// ==UserScript==
// @name         Bot for yandex
// @namespace    http://tampermonkey.net/
// @version      0.1
// @description  try to take over the world!
// @author       You
// @match        https://yandex.ru/
// @match        https://xn----7sbab5aqcbiddtdj1e1g.xn--p1ai/
// @grant        none
// ==/UserScript==


let keywords = ["Гобой", "Как звучит флейта", "Что такое валторна", "Как выглядит тромбон", "Музыкальные диктанты онлайн", "Виолончель"];
let keyword = keywords[getRandom(0,keywords.length)];
let links = document.links;

let button = document.getElementsByClassName("button mini-suggest__button")[0];
  if(button != undefined){
      writeWord(keyword);
  }

if (location.host == "yandex.ru"){
    getYandexPage();
}
else {
    if (getRandom(0,100)>20){
        let index = getRandom(0,links.length);
        if(links[index].href.indexOf('xn----7sbab5aqcbiddtdj1e1g.xn--p1ai')!=-1){
            setTimeout(()=>{links[index].click();},getRandom(2000,4000));
        }
        else location.href = 'https://xn----7sbab5aqcbiddtdj1e1g.xn--p1ai/';
    }
    else location.href = "https://yandex.ru/";
}


function getRandom(min,max){
    return Math.floor(Math.random()*(max-min)+min);
}

function writeWord(keyword){
  let i = 0;
  let timerId = setInterval(()=>{
    document.getElementsByName("text")[0].value += keyword[i];
    i++;
    if (i==keyword.length) {
        clearInterval(timerId);
        button.click();
    }
  },300);
}

