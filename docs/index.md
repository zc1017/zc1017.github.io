---
# https://vitepress.dev/reference/default-theme-home-page
layout: home

hero:
  name: "个人学习资料站点"
# text: "A VitePress Site"
  tagline: 记录的一些杂七杂八的东西
  image:
    src: /logo.svg
    alt: 张创
    width: 200
    height: 200
  actions:
    - theme: brand
      text: 开 始
      link: /linux/centos/
    - theme: alt
      text: 天王盖地虎
      link: /api-examples/
   

features:
  - icon:
      src: /index/linux.svg  
    title: Linux
    details: linux相关的一些内容
    linkText: 查看更多
    link: /linux/centos/
  - icon:
      src: /index/web.svg
      width: 40
      height: 40
    title: 前端
    details: 前端相关的一些内容
    linkText: 查看更多
    link: /frontend/gis/cesium/
  - icon:
      src: /index/code.svg
      width: 40
      height: 40
    title: 后端
    details: 后端相关的一些内容
    linkText: 查看更多
    link: https://www.baidu.com
  - icon: 
      src: /index/others.svg
      width: 40
      height: 40
    title: 杂项
    details: 杂七杂八的一些...
    linkText: 查看更多
    link: /guide/start
---

<style>
  :root {
  --vp-home-hero-name-color: transparent;
  --vp-home-hero-name-background: -webkit-linear-gradient(120deg, #bd34fe, #41d1ff);
  /* --vp-home-hero-image-background-image: linear-gradient(-45deg, #bd34fe 50%, #47caff 50%);
  --vp-home-hero-image-filter: blur(40px); */
}
.sidebar .sidebar-links {
  /* 设置侧边栏容器的高度 */
  height: 100%;
  /* 隐藏滚动条 */
  scrollbar-width: none;
  -ms-overflow-style: none;
}

.sidebar .sidebar-links::-webkit-scrollbar {
  display: none;
}
::-webkit-scrollbar {
  display: none;
}

</style>
