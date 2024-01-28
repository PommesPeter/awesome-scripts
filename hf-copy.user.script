// ==UserScript==
// @name         Huggingface URLCopy
// @namespace    http://tampermonkey.net/
// @version      2024-01-28
// @description  Copy download url from huggingface and replace with hf-mirror.com
// @author       PommesPeter
// @match        https://huggingface.co/datasets/*
// @match        https://huggingface.co/*/tree/main
// @icon         https://www.google.com/s2/favicons?sz=64&domain=huggingface.co
// @grant        none
// @license      MIT
// @run-at       document-end
// ==/UserScript==


function clickButton(url) {
    return () => {
        setTimeout(function() {
            var download_url = url.replace("blob", "resolve").replace("huggingface.co", "hf-mirror.com") + "?download=true";
            var file_name_split_list = url.split("/");
            var file_name = file_name_split_list[file_name_split_list.length - 1]
            var wget_command = `wget -c ${download_url} -O ${file_name}`
            navigator.clipboard.writeText(wget_command);
        }, 100);
    }
};


(function() {
    'use strict';
    var file_list = document.getElementsByClassName("mb-8")[0]
    setTimeout(function() {
        for (var i = 0; i < file_list.childElementCount; i++) {
            var button = document.createElement("button"); // 创建一个按钮
            var list_item = file_list.children[i];
            var list_item_col_first = list_item.children[0];
            var sub_page_url = list_item_col_first.children[0].href;
            // create a button
            button.textContent = "📄"
            button.className = "ml-2 flex h-5 w-5 items-center justify-center rounded border text-gray-500 group-hover:bg-gray-50 group-hover:text-gray-800 group-hover:shadow-sm xl:ml-4 dark:border-gray-800 dark:group-hover:bg-gray-800 dark:group-hover:text-gray-300"
            button.title = "click to copy wget command."
            button.style.width = "28px";
            button.style.height = "28px";
            button.style.align = "center";
            button.style.color = "white";
            button.style.fontSize = "14px"
            button.style.textSizeAdjust = "100%"
            button.style.background = "#ffffff";
            button.id = i;
            button.style.borderRadius = "9px";

            // add listener and button
            button.addEventListener("click", clickButton(sub_page_url));
/*             list_item_col_first.children[1].removeChild(list_item_col_first.children[1].firstChild) */
            list_item_col_first.children[1].append(button)
    }
        },4000);
})();
