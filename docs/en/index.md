---
layout: home
---

<div class='msg'>
  <div class=img><img src='/index/nodata.svg' /></div>
  <div class='tips'><a href="/" target="_self">还没有翻译内容</a></div>
</div>


<style>

.msg{
  display: flex;
  justify-content: center; /* 水平居中 */
  align-items: center;     /* 垂直居中 */
  flex-direction: column;
  position: relative;
  top:50%;
  transform:translateY(50%);

  
}
.tips{
  font-weight:bolder;
}
.img{
  max-width:40%;
}

.tips:hover{
  cursor: pointer;
}

</style>