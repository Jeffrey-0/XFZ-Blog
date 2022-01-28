---
title: AES加密笔记
---

## 简介

高级加密标准(AES,Advanced Encryption Standard)为最常见的对称加密算法，即相同密钥。

## 加密流程

![img](https://imgconvert.csdnimg.cn/aHR0cDovL2ltZy5ibG9nLmNzZG4ubmV0LzIwMTcwMjE5MDgyOTA5Njg4?x-oss-process=image/format,png)

## 使用

利用`crypto-js`进行AES加密操作
<!-- more -->
* 安装

  ```shell
  npm install --save_dev crypto-js
  ```

* 全局引用

  ```js
  // 导入 crypto-js 包 
  import cryptoJS from 'crypto-js/crypto-js'
  //把AES加密vue原型里
  Vue.prototype.$cryptoJS = cryptoJS;
  ```

* 使用

  ```js
  // 加密
  encryptionAES (params) {
      let keys = '' , encryptorStr = '';
      keys = this.$cryptoJS.enc.Utf8.parse("test_AES_test");
      params = this.$cryptoJS.enc.Utf8.parse(params);
      // 开始加密
      encryptorStr = this.$cryptoJS.AES.encrypt(
          params, 
          keys, 
          { 
              mode: this.$cryptoJS.mode.ECB, 
              padding: this.$cryptoJS.pad.Pkcs7
          }
      );
      encryptorStr = String(encryptorStr); //之将加密后的转换成 字符串, 解密成功
      //返回 加密后的 字符串
      return encryptorStr;
  }
  
  
  // 解密
  decryptAES (params) { 
      let keys = '' , decryptStr = '';
      keys = this.$cryptoJS.enc.Utf8.parse("onLineTradeTKAMC");
      // 开始解密
      decryptStr = this.$cryptoJS.AES.decrypt(
          params, 
          keys, 
          {
              mode: this.$cryptoJS.mode.ECB,
              padding: this.$cryptoJS.pad.Pkcs7
          }
      );
      decryptStr = this.$cryptoJS.enc.Utf8.stringify(decryptStr).toString();
      //返回 解密后的 字符串
      return decryptStr;
  }
  ```



