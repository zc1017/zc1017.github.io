---
layout: home
---

<div class='msg'>
  <div class=img><img src='/index/nodata.svg' /></div>
  <div class='tips'>
    <span>还没有翻译内容</span>
    <a href="/" target="_self">返回中文页</a>
  </div>
</div>


<style>

.msg{
  display: flex;
  justify-content: center; /* 水平居中 */
  align-items: center;     /* 垂直居中 */
  flex-direction: column;
  position: relative;
  top:50%;
  transform:translateY(30%);
}
.tips{
  font-weight:bolder;
}
.img{
  max-width:40%;
}
.tips span{
  padding: 10px ;
  display:block;
}
.tips a{
  display:none;
}
.tips:hover span{
  display:none;
}
.tips:hover a{
  background-color:rgb(77,107,226);
  border-radius:20px;
  cursor: pointer;
  display:block;
  padding: 10px ;
  color:white;
}

</style>
