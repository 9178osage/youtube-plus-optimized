// ==UserScript==
// @name        🔥🔥🔥文本选中复制🔥🔥🔥 (Safari 优化版)
// @description 解除网站不允许复制的限制，文本选中后点击复制按钮即可复制，主要用于 百度文库 道客巴巴 腾讯文档 豆丁网 无忧考网 学习啦 蓬勃范文 思否社区 力扣 知乎 语雀 等
// @namespace   https://github.com/WindrunnerMax/TKScript
// @version     6.2.10.1
// @author      Czy
// @match       *://wenku.baidu.com/view/*
// @match       *://wenku.baidu.com/share/*
// @match       *://wenku.baidu.com/link*
// @match       *://wenku.baidu.com/aggs/*
// @match       *://wenku.baidu.com/ndPureView/*
// @match       *://www.51test.net/show/*
// @match       *://www.xuexi.la/*
// @match       *://www.xuexila.com/*
// @match       *://www.cspengbo.com/*
// @match       *://*.doc88.com/*
// @match       *://segmentfault.com/*
// @match       *://wk.baidu.com/view/*
// @match       *://leetcode-cn.com/problems/*
// @match       *://leetcode.cn/problems/*
// @match       *://*.zhihu.com/*
// @match       *://z.30edu.com.cn/*
// @match       *://docs.qq.com/doc/*
// @match       *://docs.qq.com/sheet/*
// @match       *://docs.qq.com/slide/*
// @match       *://boke112.com/post/*
// @match       *://*.yuque.com/*
// @match       *://www.commandlinux.com/*
// @match       *://*.diyifanwen.com/*
// @match       *://*.mbalib.com/*
// @match       *://*.cnitpm.com/*
// @match       *://bbs.mihoyo.com/ys/*
// @match       *://*.ruiwen.com/*
// @match       *://www.uemeds.cn/*
// @match       *://www.oh100.com/*
// @match       *://www.aiyuke.com/news/*
// @match       *://www.fwsir.com/*
// @match       *://www.wenxm.cn/*
// @match       *://www.unjs.com/*
// @match       *://www.ahsrst.cn/*
// @match       *://*.yjbys.com/*
// @match       *://*.qidian.com/*
// @match       *://*.zongheng.com/*
// @match       *://*.17k.com/*
// @match       *://*.ciweimao.com/*
// @match       *://book.qq.com/*
// @match       *://*.360doc.com/content/*
// @match       *://*.850500.com/news/*
// @match       *://utaten.com/lyric/*
// @match       *://*.jianbiaoku.com/*
// @match       *://*.kt250.com/*
// @match       *://www.kejudati.com/*
// @match       *://*.xiaohongshu.com/discovery/*
// @match       *://*.baibeike.com/*
// @match       *://*.blog.csdn.net/*
// @match       *://*.bilibili.com/read/*
// @match       *://*.cnki.net/KXReader/*
// @match       *://*.cnrencai.com/*
// @match       *://*.kodiplayer.cn/*
// @match       *://tongxiehui.net/*
// @match       *://*.jianshu.com/p/*
// @match       *://*.linovelib.com/novel/*
// @match       *://*.wjx.cn/*
// @match       *://*.wjx.top/*
// @match       *://*.chazidian.com/*
// @match       *://*.juejin.cn/post/*
// @match       *://*.zgbk.com/ecph/*
// @match       *://*.wenmi.com/article/*
// @match       *://yuedu.baidu.com/*
// @match       *://www.inrrp.com.cn/*
// @match       *://fanyi.baidu.com/mtpe/*
// @match       *://www.shubaoc.com/*
// @match       *://blog.51cto.com/*
// @match       *://www.ximalaya.com/*
// @match       *://*.tianqi.com/*
// @match       *://*.xiexiebang.com/*
// @match       *://*.docin.com/*
// @match       *://*.ddwk8.cn/*
// @match       *://*.php.cn/*
// @match       *://cooco.net.cn/*
// @match       *://fanqienovel.com/*
// @match       *://*.mobiletrain.org/*
// @match       *://*.examcoo.com/*
// @match       *://*.rrdynb.com/*
// @match       *://*.fuwu7.com/*
// @match       *://*.xiangqiqipu.com/*
// @match       *://note.youdao.com/*
// @match       *://*.163.com/*
// @match       *://*.aipiaxi.com/*
// @match       *://wenku.csdn.net/*
// @match       *://www.kdocs.cn/*
// @match       *://www.xiaoyuzhoufm.com/*
// @match       *://*.mcmod.cn/*
// @match       *://*.zsxq.com/
// @match       *://*.volcengine.com/*
// @match       *://*.lyrical-nonsense.com/*
// @match       *://*.xueqiu.com/*
// @match       *://*.php.cn/*
// @match       *://*.51cto.com/*
// @match       *://*.educoder.net/*
// @supportURL  https://github.com/WindrunnerMax/TKScript/issues
// @license     GPL License
// @run-at      document-start
// @connect     res3.doc88.com
// @grant       unsafeWindow
// @grant       GM_xmlhttpRequest
// ==/UserScript==
(function () {
    'use strict';

    var css_248z$1 = ".__copy-button:hover{filter:brightness(1.08)!important}";

    var css_248z = "#select-tooltip,#sfModal,div[id^=reader-helper]{display:none!important}.modal-open{overflow:auto!important}._sf_adjust_body{padding-right:0!important}";

    const DOM_STAGE = {
      START: "document-start",
      END: "document-end"
    };
    const DOM_READY = "DOMContentLoaded";
    const PAGE_LOADED = "load";
    const MOUSE_UP = "mouseup";
    const MOUSE_DOWN = "mousedown";
    const MOUSE_MOVE = "mousemove";
    const COPY = "copy";
    const SELECT_START = "selectstart";
    const CONTEXT_MENU = "contextmenu";
    const KEY_DOWN = "keydown";
    const SELECTION_CHANGE = "selectionchange";

    const onDomReady = (fn) => {
      if (document.readyState !== "loading") {
        fn();
      } else {
        window.addEventListener(DOM_READY, fn, { once: true });
      }
    };
    const onWindowLoad = (fn) => {
      if (document.readyState === "complete") {
        fn();
      } else {
        window.addEventListener(PAGE_LOADED, fn, { once: true });
      }
    };

    const opt = Object.prototype.toString;
    function isString(value) {
      return opt.call(value) === "[object String]";
    }

    const dom = {
      query: function(selector) {
        return document.querySelector(selector);
      },
      attr: function(selector, attr, value) {
        const dom2 = document.querySelector(selector);
        dom2 && dom2.setAttribute(attr, value);
      },
      append: function(selector, content) {
        const container = document.createElement("div");
        if (isString(content)) {
          container.innerHTML = content;
        } else {
          container.appendChild(content);
        }
        const targetDOM = document.querySelector(selector);
        targetDOM && targetDOM.append(container);
        return container;
      },
      remove: function(selector) {
        const targetDOM = document.querySelector(selector);
        targetDOM && targetDOM.remove();
      }
    };

    const appendStyle = (css) => {
      const style = document.createElement("style");
      style.textContent = css;
      const root = document.head || document.documentElement;
      if (root) {
        root.appendChild(style);
      } else {
        onDomReady(() => (document.head || document.documentElement).appendChild(style));
      }
    };
    const whenElement = (selector, callback, timeout = 15e3) => {
      const found = document.querySelector(selector);
      if (found) {
        callback(found);
        return void 0;
      }
      let debounce = 0;
      let observer = null;
      const stop = () => {
        clearTimeout(debounce);
        clearTimeout(giveUp);
        observer && observer.disconnect();
      };
      const giveUp = setTimeout(stop, timeout);
      observer = new MutationObserver(() => {
        if (debounce)
          return void 0;
        debounce = setTimeout(() => {
          debounce = 0;
          const target = document.querySelector(selector);
          if (target) {
            stop();
            callback(target);
          }
        }, 300);
      });
      observer.observe(document.documentElement || document, { childList: true, subtree: true });
    };
    const isCopyShortcut = (e) => {
      return (e.ctrlKey || e.metaKey) && typeof e.key === "string" && e.key.toUpperCase() === "C";
    };

    const initBaseEvent = (websiteConfig) => {
      onDomReady(() => {
        if (websiteConfig.initCopyEvent) {
          const stop = (e) => e.stopPropagation();
          document.oncopy = stop;
          document.addEventListener(COPY, stop);
          if (document.body) {
            document.body.oncopy = stop;
            document.body.addEventListener(COPY, stop);
          }
        }
      });
    };
    const initBaseStyle = () => {
      appendStyle(css_248z$1);
      appendStyle(css_248z);
    };

    /*!
     * 外部引用 static.doc88.com 声明
     * 此部分是在处理 doc88.com 才会加载的资源文件，此资源文件由该网站加载时提供
     */
    let path = "";
    const website$u = {
      regexp: /.*doc88\.com\/.+/,
      init: () => {
        dom.append(
          "body",
          `<style id="copy-element-hide">#left-menu{display: none !important;}</style>`
        );
        GM_xmlhttpRequest({
          method: "GET",
          url: "https://res3.doc88.com/resources/js/modules/main-v2.min.js?v=3.55",
          onload: function(response) {
            const result = /\("#cp_textarea"\).val\(([\S]*?)\);/.exec(response.responseText);
            if (result)
              path = result[1];
          }
        });
        onWindowLoad(() => {
          const cpFn = unsafeWindow.copyText ? unsafeWindow.copyText.toString() : "";
          const fnResult = /<textarea[\s\S]*?>'\+([\S]*?)\+"<\/textarea>/.exec(cpFn);
          if (fnResult)
            path = fnResult[1];
        });
      },
      getSelectedText: () => {
        let select = unsafeWindow;
        path.split(".").forEach((v) => {
          select = select[v];
        });
        if (!select) {
          unsafeWindow.Config.vip = 1;
          unsafeWindow.Config.logined = 1;
          dom.remove("#copy-element-hide");
        }
        return select;
      }
    };

    const website$t = {
      regexp: /.*segmentfault\.com\/.+/,
      init: function() {
        const body = dom.query("body");
        if (body) {
          body.classList.add("_sf_adjust_body");
          body.onclick = () => {
            body.style.paddingRight = "0";
          };
        }
      }
    };

    const TEXT_PLAIN = "text/plain";
    const TEXT_HTML = "text/html";
    const execCopyCommand = (data) => {
      const textarea = document.createElement("textarea");
      const handler = (event) => {
        event.preventDefault();
        event.stopImmediatePropagation();
        for (const [key, value] of Object.entries(data)) {
          event.clipboardData && event.clipboardData.setData(key, value);
        }
      };
      const selection = window.getSelection();
      const ranges = [];
      if (selection) {
        for (let i = 0; i < selection.rangeCount; i++) {
          ranges.push(selection.getRangeAt(i));
        }
      }
      const active = document.activeElement;
      textarea.addEventListener(COPY, handler, true);
      textarea.style.cssText = "position:fixed;left:-9999px;top:0;width:1px;height:1px;opacity:0;pointer-events:none";
      textarea.value = data[TEXT_PLAIN] || " ";
      (document.body || document.documentElement).appendChild(textarea);
      let success = false;
      try {
        textarea.select();
        success = document.execCommand("copy");
      } catch (error) {
        success = false;
      } finally {
        textarea.removeEventListener(COPY, handler, true);
        textarea.remove();
        if (selection) {
          selection.removeAllRanges();
          ranges.forEach((range) => selection.addRange(range));
        }
        if (active && active !== document.body && typeof active.focus === "function") {
          try {
            active.focus({ preventScroll: true });
          } catch (error) {
            console.warn("[copy] restore focus failed", error);
          }
        }
      }
      return success;
    };
    const getPlainText = (data) => {
      if (!data)
        return "";
      return String((isString(data) ? data : data[TEXT_PLAIN]) || "");
    };
    const isEmptyContent = (data) => {
      return !getPlainText(data).trim();
    };
    const copy = (data) => {
      if (isEmptyContent(data))
        return Promise.resolve(false);
      const params = isString(data) ? { [TEXT_PLAIN]: data } : data;
      const fallback = () => {
        try {
          return Promise.resolve(execCopyCommand(params));
        } catch (error) {
          return Promise.resolve(false);
        }
      };
      if (navigator.clipboard && window.ClipboardItem) {
        try {
          const dataItems = {};
          for (const [key, value] of Object.entries(params)) {
            if (!value && key !== TEXT_PLAIN)
              continue;
            dataItems[key] = new Blob([value], { type: key });
          }
          return navigator.clipboard.write([new ClipboardItem(dataItems)]).then(() => true, fallback);
        } catch (error) {
          return fallback();
        }
      }
      return fallback();
    };

    const BUTTON_COLOR = "#4c98f7";
    const BUTTON_SHOW = "opacity .15s,visibility 0s";
    const BUTTON_HIDE = "opacity .15s,visibility 0s linear .15s";
    const BUTTON_STYLE = [
      "all:initial",
      "position:absolute",
      "left:0",
      "top:0",
      "z-index:2147483647",
      "display:flex",
      "align-items:center",
      "justify-content:center",
      "box-sizing:border-box",
      "min-width:60px",
      "height:30px",
      "margin:0",
      "padding:0 12px",
      "border-radius:4px",
      `background:${BUTTON_COLOR}`,
      "color:#fff",
      "font:13px/1 -apple-system,BlinkMacSystemFont,'PingFang SC','Helvetica Neue',Arial,sans-serif",
      "white-space:nowrap",
      "cursor:pointer",
      "-webkit-user-select:none",
      "user-select:none",
      "box-shadow:0 2px 8px rgba(0,0,0,.25)",
      "visibility:hidden",
      "opacity:0",
      "pointer-events:none",
      `transition:${BUTTON_HIDE}`
    ].join(";");
    const placeButton = (el, event) => {
      const margin = 8;
      const gap = 30;
      const root = document.documentElement;
      const viewWidth = root.clientWidth || window.innerWidth;
      const viewHeight = root.clientHeight || window.innerHeight;
      const width = el.offsetWidth || 60;
      const height = el.offsetHeight || 30;
      const pointerX = Number.isFinite(event.clientX) ? event.clientX : 0;
      const pointerY = Number.isFinite(event.clientY) ? event.clientY : 0;
      let x = pointerX + gap;
      if (x + width + margin > viewWidth)
        x = pointerX - gap - width;
      x = Math.max(margin, Math.min(x, viewWidth - width - margin));
      const y = Math.max(margin, Math.min(pointerY, viewHeight - height - margin));
      const left = x + (window.pageXOffset || 0);
      const top = y + (window.pageYOffset || 0);
      el.style.left = `${left}px`;
      el.style.top = `${top}px`;
      const rect = el.getBoundingClientRect();
      if (Math.abs(rect.left - x) > 1 || Math.abs(rect.top - y) > 1) {
        el.style.left = `${left + x - rect.left}px`;
        el.style.top = `${top + y - rect.top}px`;
      }
    };

    class Instance {
      constructor() {
        this.id = "__copy";
        this.className = "__copy-button";
        this.dom = null;
        this.content = null;
        this.disabled = false;
        this.visible = false;
        this.busy = false;
        this.pressing = false;
        this.timer = 0;
        this.enable = () => {
          this.disabled = false;
          if (this.dom)
            this.dom.style.display = "flex";
        };
        this.disable = () => {
          this.disabled = true;
          this.hide();
          if (this.dom)
            this.dom.style.display = "none";
        };
        this.destroy = () => {
          clearTimeout(this.timer);
          this.dom && this.dom.remove();
          this.dom = null;
          this.visible = false;
          this.busy = false;
        };
        this.mount = () => {
          const el = this.dom;
          if (!el || el.isConnected)
            return void 0;
          const parent = document.body || document.documentElement;
          if (parent) {
            parent.appendChild(el);
          } else {
            window.addEventListener(DOM_READY, this.mount, { once: true });
          }
        };
        this.init = (name) => {
          const container = document.createElement("div");
          container.id = this.id;
          container.className = this.className;
          container.style.cssText = BUTTON_STYLE;
          container.textContent = name || "复制";
          if (this.disabled)
            container.style.display = "none";
          container.addEventListener("mouseup", (e) => e.stopPropagation(), true);
          container.addEventListener(
            "mousedown",
            (e) => {
              e.stopPropagation();
              e.preventDefault();
            },
            true
          );
          container.addEventListener("click", (e) => {
            e.stopPropagation();
            e.preventDefault();
            this.copyNow();
          });
          this.dom = container;
          this.mount();
        };
        this.getInstance = () => {
          if (this.dom === null) {
            this.init();
          } else if (!this.dom.isConnected) {
            this.mount();
          }
          return this.dom;
        };
        this.show = (event) => {
          if (this.disabled)
            return void 0;
          const el = this.getInstance();
          clearTimeout(this.timer);
          this.busy = false;
          this.visible = true;
          el.textContent = "复制";
          el.style.background = BUTTON_COLOR;
          placeButton(el, event);
          el.style.transition = BUTTON_SHOW;
          el.style.visibility = "visible";
          el.style.opacity = "1";
          el.style.pointerEvents = "auto";
        };
        this.hide = () => {
          clearTimeout(this.timer);
          this.busy = false;
          this.visible = false;
          const el = this.dom;
          if (!el)
            return void 0;
          el.style.transition = BUTTON_HIDE;
          el.style.opacity = "0";
          el.style.visibility = "hidden";
          el.style.pointerEvents = "none";
        };
        this.feedback = (success) => {
          const el = this.dom;
          if (!el || !this.busy)
            return void 0;
          clearTimeout(this.timer);
          el.textContent = success ? "已复制 ✓" : "复制失败";
          el.style.background = success ? "#2ea44f" : "#d1242f";
          this.timer = setTimeout(this.hide, success ? 900 : 1800);
        };
        this.copyNow = () => {
          if (this.busy || isEmptyContent(this.content))
            return void 0;
          this.busy = true;
          clearTimeout(this.timer);
          this.timer = setTimeout(this.hide, 2500);
          copy(this.content).then(this.feedback, () => this.feedback(false));
        };
        this.onCopy = (content, event) => {
          this.content = content;
          this.show(event);
        };
      }
    }
    const instance = new Instance();

    const stopNativePropagation = (event2) => {
      event2.stopPropagation();
    };
    const event = {
      hideButton: () => {
        instance.disable();
      },
      showButton: () => {
        instance.enable();
      },
      removeAttributes: (selector, attr = []) => {
        const dom = isString(selector) ? document.querySelector(selector) : selector;
        dom && attr.forEach((item) => dom.removeAttribute(item));
      },
      enableUserSelectByCSS: () => {
        appendStyle("*{user-select: auto !important;-webkit-user-select: auto !important;}");
      },
      enableOnSelectStart: (selector) => {
        whenElement(selector, (el) => el.addEventListener(SELECT_START, stopNativePropagation));
      },
      enableOnContextMenu: (selector) => {
        whenElement(selector, (el) => el.addEventListener(CONTEXT_MENU, stopNativePropagation));
      },
      enableOnCopy: (selector) => {
        whenElement(selector, (el) => el.addEventListener(COPY, stopNativePropagation));
      },
      enableOnKeyDown: (selector) => {
        whenElement(selector, (el) => {
          el.addEventListener(KEY_DOWN, (e) => {
            if (isCopyShortcut(e))
              return e.stopPropagation();
          });
        });
      },
      enableOnSelectStartByCapture: () => {
        window.addEventListener(SELECT_START, stopNativePropagation, true);
        document.addEventListener(SELECT_START, stopNativePropagation, true);
      },
      enableOnContextMenuByCapture: () => {
        window.addEventListener(CONTEXT_MENU, stopNativePropagation, true);
        document.addEventListener(CONTEXT_MENU, stopNativePropagation, true);
      },
      enableOnCopyByCapture: () => {
        window.addEventListener(COPY, stopNativePropagation, true);
        document.addEventListener(COPY, stopNativePropagation, true);
      },
      enableOnKeyDownByCapture: () => {
        document.addEventListener(
          KEY_DOWN,
          (e) => isCopyShortcut(e) && e.stopPropagation(),
          true
        );
      }
    };

    const website$s = {
      regexp: /.*wk\.baidu\.com\/view\/.+/,
      init: function() {
        event.hideButton();
        event.enableOnSelectStartByCapture();
        onWindowLoad(() => {
          dom.attr(".sf-edu-wenku-vw-container", "style", "");
        });
      }
    };

    const website$r = {
      regexp: /.*zhihu\.com\/.*/,
      init: function() {
        event.hideButton();
        event.enableUserSelectByCSS();
        event.enableOnCopyByCapture();
        if (location.hostname === "zhuanlan.zhihu.com") {
          const removeFocalPointModal = (mutationsList) => {
            for (const mutation of mutationsList) {
              const addedNodes = mutation.addedNodes;
              for (let i = 0; i < addedNodes.length; i++) {
                const target = addedNodes[i];
                if (target.nodeType != 1)
                  continue;
                if (target instanceof HTMLDivElement && target.querySelector("[data-focus-scope-start]")) {
                  const element = target.querySelector("[data-focus-scope-start]");
                  element && element.parentElement && element.parentElement.textContent && element.parentElement.textContent.indexOf("立即登录/注册") > -1 && element.parentElement.parentElement && element.parentElement.parentElement.removeChild(element.parentElement);
                }
              }
            }
          };
          const observer = new MutationObserver(removeFocalPointModal);
          observer.observe(document, { childList: true, subtree: true });
        }
      }
    };

    const website$q = {
      regexp: /.*30edu\.com\.cn\/.+/,
      init: function() {
        onWindowLoad(() => {
          var _a;
          const iframes = document.getElementsByTagName("iframe");
          if (iframes.length === 2) {
            const body = (_a = iframes[1].contentWindow) == null ? void 0 : _a.document.querySelector("body");
            body && event.removeAttributes(body, ["oncopy", "oncontextmenu", "onselectstart"]);
          }
        });
      }
    };

    const website$p = {
      regexp: /.*docs\.qq\.com\/(doc|sheet)\/.+/,
      config: {
        initCopyEvent: false,
        captureInstance: true,
        delay: 100
      },
      init: function() {
        onWindowLoad(() => {
          instance.disable();
        });
      },
      getSelectedText: function() {
        var _a;
        if (unsafeWindow.pad && unsafeWindow.pad.editor && !unsafeWindow.pad.editor.isCopyable()) {
          instance.enable();
          const editor = unsafeWindow.pad.editor;
          if (editor.getCopyContent) {
            const content = editor.getCopyContent() || {};
            const plainText = content.plain || "";
            const htmlText = content.html || "";
            return {
              [TEXT_PLAIN]: plainText,
              [TEXT_HTML]: htmlText
            };
          } else {
            editor._docEnv.copyable = true;
            editor.clipboardManager.copy();
            const plainText = editor.clipboardManager.customClipboard.plain || "";
            const htmlText = editor.clipboardManager.customClipboard.html || "";
            editor._docEnv.copyable = false;
            return {
              [TEXT_PLAIN]: plainText,
              [TEXT_HTML]: htmlText
            };
          }
        }
        const sheetStatus = unsafeWindow.SpreadsheetApp ? unsafeWindow.SpreadsheetApp.permissions ? unsafeWindow.SpreadsheetApp.permissions.sheetStatus : unsafeWindow.SpreadsheetApp.sheetStatus : null;
        if (sheetStatus && sheetStatus.canCopy === false && sheetStatus.canEdit && sheetStatus.canEdit() === false) {
          instance.enable();
          const SpreadsheetApp = unsafeWindow.SpreadsheetApp;
          const [selection] = SpreadsheetApp.view.getSelectionRanges();
          if (selection) {
            const text = [];
            const { startColIndex, startRowIndex, endColIndex, endRowIndex } = selection;
            for (let i = startRowIndex; i <= endRowIndex; i++) {
              for (let k = startColIndex; k <= endColIndex; k++) {
                const cell = SpreadsheetApp.workbook.activeSheet.getCellDataAtPosition(i, k);
                if (!cell)
                  continue;
                text.push(" ", ((_a = cell.formattedValue) == null ? void 0 : _a.value) || cell.value || "");
              }
              i !== endRowIndex && text.push("\n");
            }
            const str = text.join("");
            return /^\s*$/.test(str) ? "" : str;
          }
        }
        return "";
      }
    };

    const website$o = {
      regexp: /.*docs\.qq\.com\/slide\/.+/,
      config: {
        initCopyEvent: false,
        captureInstance: true,
        runAt: "document-start"
      },
      init: function() {
        let webpackJsonp = unsafeWindow.webpackJsonp;
        Object.defineProperty(unsafeWindow, "webpackJsonp", {
          get() {
            return webpackJsonp;
          },
          set(newValue) {
            if (newValue.push.__HOOKED__) {
              return;
            }
            webpackJsonp = newValue;
            const originPush = webpackJsonp.push;
            function push(...args) {
              const [, mods] = args[0];
              for (const [key, fn] of Object.entries(mods)) {
                const stringifyFn = String(fn);
                if (/this\.shouldResponseCopy\(/.test(stringifyFn)) {
                  const next = stringifyFn.replace(/this\.shouldResponseCopy\(/g, "(() => true)(");
                  mods[key] = new Function(`return (${next})`)();
                }
              }
              return originPush.call(this, ...args);
            }
            push.__HOOKED__ = 1;
            webpackJsonp.push = push;
          }
        });
        onWindowLoad(() => {
          instance.disable();
        });
      }
    };

    const website$n = {
      regexp: new RegExp(".+://boke112.com/post/.+"),
      init: function() {
        event.enableOnCopyByCapture();
        const template = `
            <style>
                :not(input):not(textarea)::selection {
                    background-color: #2440B3 !important;
                    color: #fff !important;
                }

                :not(input):not(textarea)::-moz-selection {
                    background-color: #2440B3 !important;
                    color: #fff !important;
                }
            </style>
        `;
        dom.append("head", template);
      }
    };

    const website$m = {
      regexp: /diyifanwen/,
      init: function() {
        event.hideButton();
        event.enableOnCopyByCapture();
        event.enableOnKeyDownByCapture();
      }
    };

    const website$l = {
      regexp: /mbalib/,
      init: function() {
        onWindowLoad(() => {
          event.removeAttributes("fullScreenContainer", ["oncopy", "oncontextmenu", "onselectstart"]);
        });
      }
    };

    const website$k = {
      regexp: /cnitpm/,
      init: function() {
        event.hideButton();
        onWindowLoad(() => {
          event.removeAttributes("body", ["oncopy", "oncontextmenu", "onselectstart"]);
        });
      }
    };

    const website$j = {
      regexp: new RegExp(".+bbs.mihoyo.com/.+"),
      init: function() {
        event.hideButton();
        event.enableOnCopyByCapture();
        event.enableOnSelectStartByCapture();
        event.enableUserSelectByCSS();
      }
    };

    const website$i = {
      regexp: new RegExp(".+www.uemeds.cn/.+"),
      init: function() {
        event.hideButton();
        event.enableUserSelectByCSS();
      }
    };

    const website$h = {
      regexp: new RegExp(".+aiyuke.com/news/.+"),
      init: function() {
        event.hideButton();
        event.enableUserSelectByCSS();
      }
    };

    const website$g = {
      regexp: new RegExp("qidian"),
      init: function() {
        event.hideButton();
        event.enableUserSelectByCSS();
        event.enableOnCopy(".main-read-container");
        event.enableOnContextMenu(".main-read-container");
      }
    };

    const website$f = {
      regexp: new RegExp("zongheng"),
      init: function() {
        event.removeAttributes(".reader_box", ["style", "unselectable", "onselectstart"]);
        event.removeAttributes(".reader_main", ["style", "unselectable", "onselectstart"]);
        event.hideButton();
        event.enableOnKeyDown("body");
        event.enableUserSelectByCSS();
        event.enableOnCopy(".content");
        event.enableOnContextMenu("body");
        event.enableOnSelectStart(".content");
      }
    };

    const website$e = {
      regexp: new RegExp("17k"),
      init: () => {
        event.hideButton();
        event.enableOnCopy(".readAreaBox .p");
      }
    };

    const website$d = {
      regexp: new RegExp("ciweimao"),
      init: function() {
        event.hideButton();
        event.enableUserSelectByCSS();
        event.enableOnCopy("#J_BookCnt");
        event.enableOnContextMenu("body");
        event.enableOnSelectStart("#J_BookCnt");
      }
    };

    const website$c = {
      regexp: new RegExp("book\\.qq"),
      init: function() {
        event.hideButton();
        event.enableOnCopy("body");
        event.enableUserSelectByCSS();
        event.enableOnContextMenu("body");
        event.enableOnSelectStart("body");
      }
    };

    const website$b = {
      regexp: new RegExp("utaten"),
      init: function() {
        event.hideButton();
        event.enableUserSelectByCSS();
        event.enableOnSelectStartByCapture();
      }
    };

    let preSelectedText = "";
    let curSelectedText = "";
    const website$a = {
      config: {
        runAt: "document-start"
      },
      regexp: new RegExp("wenku.baidu.com/(view|link|aggs).*"),
      init: function() {
        dom.append("head", `<style>@media print { body{ display:block; } }</style>`);
        let canvasDataGroup = [];
        const originObject = {
          context2DPrototype: unsafeWindow.document.createElement("canvas").getContext("2d").__proto__
        };
        document.createElement = new Proxy(document.createElement, {
          apply: function(target, thisArg, argumentsList) {
            const element = Reflect.apply(target, thisArg, argumentsList);
            if (argumentsList[0] === "canvas") {
              const tmpData = {
                canvas: element,
                data: []
              };
              element.getContext("2d").fillText = function(...args) {
                tmpData.data.push(args);
                originObject.context2DPrototype.fillText.apply(this, args);
              };
              canvasDataGroup.push(tmpData);
            }
            return element;
          }
        });
        let pageData = {};
        Object.defineProperty(unsafeWindow, "pageData", {
          set: (v) => pageData = v,
          get: function() {
            if (!pageData.vipInfo)
              return pageData.vipInfo = {};
            pageData.vipInfo.global_svip_status = 1;
            pageData.vipInfo.global_vip_status = 1;
            pageData.vipInfo.isVip = 1;
            pageData.vipInfo.isWenkuVip = 1;
            return pageData;
          }
        });
        const templateCSS = [
          "<style id='copy-template-css'>",
          "body{overflow: hidden !important}",
          "#copy-template-html{position: fixed; top: 0; right: 0; bottom: 0; left: 0; display: flex; align-items: center; justify-content: center;z-index: 999999; background: rgba(0,0,0,0.5);}",
          "#copy-template-html > .template-container{height: 80%; width: 80%; background: #fff; }",
          ".template-container > .title-container{display: flex; align-items: center; justify-content: space-between;padding: 10px;border-bottom: 1px solid #eee;}",
          "#copy-template-text{height: 100%; width: 100%;position: relative; overflow: auto;background: #fff;}",
          "#copy-template-html #template-close{cursor: pointer;}",
          "</style>"
        ].join("");
        const render = () => {
          canvasDataGroup = canvasDataGroup.filter((item) => item.canvas.id);
          const templateText = canvasDataGroup.map((canvasData, index) => {
            const computedTop = index * Number(canvasData.canvas.clientHeight);
            const textItem = canvasData.data.map(
              (item) => `<div style="position: absolute; left: ${item[1]}px; top: ${item[2] + computedTop}px">${item[0]}</div>`
            );
            return textItem.join("");
          });
          const templateHTML = [
            "<div id='copy-template-html'>",
            "<div class='template-container'>",
            "<div class='title-container'>",
            "<div>请自行复制</div>",
            "<div id='template-close'>关闭</div>",
            "</div>",
            "<div id='copy-template-text'>",
            templateText.join(""),
            "</div>",
            "</div>",
            "</div>"
          ].join("");
          dom.append("body", templateHTML);
          dom.append("body", templateCSS);
          const closeButton = document.querySelector("#copy-template-html #template-close");
          const close = () => {
            dom.remove("#copy-template-html");
            dom.remove("#copy-template-css");
            closeButton && closeButton.removeEventListener("click", close);
          };
          closeButton && closeButton.addEventListener("click", close);
        };
        onDomReady(() => {
          dom.append(
            "head",
            `<style>#copy-btn-wk{padding: 10px; background: rgba(0,0,0,0.5);position: fixed; left:0; top: 40%;cursor: pointer;color: #fff; z-index: 99999;}</style>`
          );
          dom.append("body", "<div id='copy-btn-wk'>复制</div>");
          const btn = dom.query("#copy-btn-wk");
          btn && (btn.onclick = render);
        });
      },
      getSelectedText: () => {
        if (window.getSelection && (window.getSelection() || "").toString()) {
          return (window.getSelection() || "").toString();
        }
        try {
          const elements = unsafeWindow.document.querySelectorAll("#app > div");
          for (const item of elements) {
            const vue = item.__vue__;
            if (vue) {
              const text = vue.$store.getters["readerPlugin/selectedTextTrim"];
              text && (curSelectedText = text);
              break;
            }
          }
        } catch (error) {
          console.warn("GET TEXT FAIL", error);
        }
        if (!curSelectedText) {
          const result = /查看全部包含“([\s\S]*?)”的文档/.exec(document.body.innerHTML);
          result && result[1] && (curSelectedText = result[1]);
        }
        if (curSelectedText && preSelectedText !== curSelectedText) {
          preSelectedText = curSelectedText;
          return curSelectedText;
        }
        return "";
      }
    };

    const website$9 = {
      regexp: new RegExp("xiaohongshu"),
      init: function() {
        event.hideButton();
        event.enableUserSelectByCSS();
        event.enableOnKeyDownByCapture();
      }
    };

    const website$8 = {
      regexp: new RegExp("leetcode"),
      init: function() {
        event.hideButton();
        onWindowLoad(() => {
          event.enableOnCopy("#lc-home");
          event.enableOnCopy("[data-layout-path='/ts0/t1']");
        });
      }
    };

    const website$7 = {
      regexp: /csdn/,
      init: function() {
        event.hideButton();
        event.enableOnCopyByCapture();
        event.enableUserSelectByCSS();
      }
    };

    const website$6 = {
      regexp: new RegExp("bilibili"),
      init: function() {
        event.hideButton();
        event.enableOnCopyByCapture();
      }
    };

    const website$5 = {
      regexp: new RegExp("cnki"),
      init: function() {
        event.hideButton();
        event.enableOnContextMenuByCapture();
        event.enableOnKeyDownByCapture();
        event.enableOnCopyByCapture();
      }
    };

    const website$4 = {
      regexp: new RegExp("docin.com/.*"),
      config: {
        initCopyEvent: false,
        captureInstance: true,
        delay: 100
      },
      init: function() {
        onWindowLoad(() => {
          var _a;
          return (_a = dom.query("#j_select")) == null ? void 0 : _a.click();
        });
        dom.append("head", "<style>#reader-copy-el{display: none;}</style>");
      },
      getSelectedText: function() {
        if (unsafeWindow.docinReader && unsafeWindow.docinReader.st) {
          return unsafeWindow.docinReader.st;
        }
        return "";
      }
    };

    const website$3 = {
      config: {
        initCopyEvent: false
      },
      regexp: /note\.youdao\.com\/newEditorV1\/bulb\.html.*/,
      init: function() {
        event.hideButton();
        let parentHref = "";
        try {
          parentHref = window.parent ? window.parent.location.href : "";
        } catch (error) {
          parentHref = "";
        }
        if (parentHref.indexOf("ynoteshare") > -1) {
          event.enableUserSelectByCSS();
          document.addEventListener(MOUSE_DOWN, stopNativePropagation, true);
          document.addEventListener(MOUSE_MOVE, stopNativePropagation, true);
        }
      }
    };

    const website$2 = {
      regexp: new RegExp(
        [
          "commandlinux",
          "cnki",
          "ruiwen",
          "oh100",
          "fwsir",
          "wenxm",
          "unjs",
          "ahsrst",
          "yjbys",
          "360doc",
          "850500",
          "jianbiaoku",
          "kt250",
          "kejudati",
          "baibeike",
          "yuque",
          "cnrencai",
          "kodiplayer",
          "tongxiehui",
          "ndPureView",
          "jianshu",
          "linovelib",
          "chazidian",
          "juejin",
          "zgbk",
          "wenmi",
          "yuedu\\.baidu",
          "inrrp",
          "shubaoc",
          "51cto",
          "ximalaya",
          "xiexiebang",
          "ddwk8",
          "php\\.cn",
          "fanqienovel\\.com/reader",
          "cooco\\.net\\.cn",
          "mobiletrain",
          "xiangqiqipu",
          "m\\.163\\.com",
          "aipiaxi",
          "wenku\\.csdn\\.net",
          "xiaoyuzhoufm\\.com",
          "mcmod\\.cn",
          "zsxq\\.com",
          "volcengine\\.com",
          "lyrical-nonsense\\.com",
          "xueqiu\\.com",
          "php\\.cn",
          "51cto\\.com",
          "educoder\\.net"
        ].join("|")
      ),
      init: function() {
        event.hideButton();
        event.enableUserSelectByCSS();
        event.enableOnCopyByCapture();
      }
    };

    const website$1 = {
      regexp: new RegExp(["wjx", "fanyi\\.baidu", "tianqi", "rrdynb", "fuwu7"].join("|")),
      init: function() {
        event.hideButton();
        event.enableUserSelectByCSS();
        event.enableOnCopyByCapture();
        event.enableOnKeyDownByCapture();
        event.enableOnSelectStartByCapture();
        event.enableOnContextMenuByCapture();
      }
    };

    const website = {
      config: {
        runAt: DOM_STAGE.START
      },
      regexp: new RegExp(["examcoo"].join("|")),
      init: function() {
        event.hideButton();
        event.enableUserSelectByCSS();
        event.enableOnCopyByCapture();
        event.enableOnKeyDownByCapture();
        event.enableOnSelectStartByCapture();
        event.enableOnContextMenuByCapture();
      }
    };

    const kdoc = {
      config: {
        runAt: DOM_STAGE.START
      },
      regexp: new RegExp("kdocs"),
      init: function() {
        const patch = () => {
          unsafeWindow.APP && (unsafeWindow.APP.canCopy = () => true);
        };
        if (unsafeWindow.APP) {
          patch();
        } else {
          let APP = void 0;
          Object.defineProperty(unsafeWindow, "APP", {
            configurable: false,
            set: (value) => {
              APP = value;
              value && patch();
            },
            get: () => APP
          });
        }
      }
    };

    const websites = [
      website$t,
      website$s,
      website$r,
      website$q,
      website$o,
      website$p,
      website$n,
      website$m,
      website$l,
      website$k,
      website$j,
      website$i,
      website$h,
      website$g,
      website$f,
      website$e,
      website$d,
      website$c,
      website$b,
      website$a,
      website$9,
      website$u,
      website$8,
      website$7,
      website$6,
      website$5,
      website$4,
      website$3,
      kdoc,
      website$2,
      website$1,
      website
    ];

    let siteGetSelectedText = null;
    const initWebsite = () => {
      let websiteConfig = {
        initCopyEvent: true,
        runAt: DOM_STAGE.END,
        captureInstance: false,
        delay: 0
      };
      const mather = (regex, website) => {
        if (regex.test(window.location.href)) {
          if (website.config) {
            websiteConfig = Object.assign(websiteConfig, website.config);
          }
          if (website.getSelectedText) {
            siteGetSelectedText = website.getSelectedText;
          }
          const init = () => {
            try {
              website.init();
            } catch (error) {
              console.warn("[copy] website init failed", error);
            }
          };
          websiteConfig.runAt === DOM_STAGE.END ? onDomReady(init) : init();
          return true;
        }
        return false;
      };
      websites.some((website) => mather(website.regexp, website));
      return websiteConfig;
    };
    const getSelectedText = () => {
      if (siteGetSelectedText)
        return siteGetSelectedText();
      if (window.getSelection)
        return (window.getSelection() || "").toString();
      if (document.getSelection)
        return (document.getSelection() || "").toString();
      if (document.selection)
        return document.selection.createRange().text;
      return "";
    };

    (function() {
      const websiteConfig = initWebsite();
      initBaseEvent(websiteConfig);
      initBaseStyle();
      const hasSiteSelection = !!siteGetSelectedText;
      const readContent = () => {
        try {
          return getSelectedText();
        } catch (error) {
          return "";
        }
      };
      const showContent = (e) => {
        const content = readContent();
        if (isEmptyContent(content)) {
          instance.hide();
          return void 0;
        }
        instance.onCopy(content, e);
      };
      window.addEventListener(
        MOUSE_UP,
        (e) => {
          instance.pressing = false;
          if (e.target === instance.dom)
            return void 0;
          if (hasSiteSelection) {
            websiteConfig.delay ? setTimeout(() => showContent(e), websiteConfig.delay) : showContent(e);
            return void 0;
          }
          if (e.button !== 0 || instance.disabled)
            return void 0;
          setTimeout(() => showContent(e), 0);
        },
        hasSiteSelection ? websiteConfig.captureInstance : true
      );
      if (!hasSiteSelection) {
        window.addEventListener(
          MOUSE_DOWN,
          (e) => {
            instance.pressing = e.target === instance.dom;
          },
          true
        );
        document.addEventListener(SELECTION_CHANGE, () => {
          if (!instance.visible || instance.busy || instance.pressing)
            return void 0;
          const selection = window.getSelection();
          const text = selection ? selection.toString() : "";
          if (isEmptyContent(text) || text !== getPlainText(instance.content)) {
            instance.hide();
          }
        });
      }
    })();

}());
