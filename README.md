# vue-scroll-prevent
vue遮罩层出现禁止穿透遮罩滚动页面

## 前端经常遇到的问题之————弹出层的滚动会穿透背景的滚动
两种情况
  - 弹出层需要滚动
  - 弹出层不需要滚动
网上找了几种方法，试了一下 都有各自bug，我就改良了一下，暂时没有bug

## code
```vue

<script>
// 全局js
  const ModalHelper = ( (bodyCls) =>{
  let scrollTop;
  return {
    afterOpen: function () {
      document.body.classList.add(bodyCls);
      document.body.style.top = 0;
    },
    beforeClose: function () {
      document.body.classList.remove(bodyCls);
      document.scrollingElement.scrollTop = 0;
    }
  };
})('popup-open');
</script>

<style lang='stylus'>
  body.popup-open {
    position fixed
    width 100%
  }
</style>

// 在使用组件弹出层的地方 调用ModalHelper 的方法，弹出后 调用 ModalHelper.afterOpen(); 关闭前 调用 ModalHelper.beforeClose();
togglePopup(list, title) {
  vm.showPopup = !vm.showPopup;
  if (!vm.showPopup) {
    vm.$public.ModalHelper.beforeClose();
  }
  if(vm.showPopup) {
    vm.$public.ModalHelper.afterOpen();
    vm.currentPopupList = [...list];
    vm.currentPopupTitle = title;
  }
}
```  

希望对各位小伙伴有帮助！ 
##                  let's rock!
