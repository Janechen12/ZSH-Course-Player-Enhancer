# ZSH-Course-Player-Enhancer
中山医院课程平台：2倍速 + 移除失焦暂停；进度条拖动
// 1. 移除离开页面时自动暂停的监听
window.removedVideoBlur = [];

for (const item of getEventListeners(window).blur || []) {
  if (item.listener.toString().includes('离开页面，视频播放被暂停')) {
    window.removeEventListener('blur', item.listener, item.useCapture);
    window.removedVideoBlur.push(item);
  }
}

// 2. 取消视频暂停函数的调试断点
undebug(HTMLMediaElement.prototype.pause);

// 3. 强制保持2倍速
const p = HTMLMediaElement.prototype;
const d = Object.getOwnPropertyDescriptor(p, 'playbackRate');

Object.defineProperty(p, 'playbackRate', {
  ...d,
  set(v) {
    d.set.call(this, Number(v) === 1 ? 2 : v);
  }
});

// 4. 设置当前视频为2倍速
document.querySelectorAll('video').forEach(v => {
  v.playbackRate = 2;
});

console.log('设置完成！');
console.log('已移除失焦监听：', window.removedVideoBlur.length);
console.log('当前视频倍速：', [...document.querySelectorAll('video')].map(v => v.playbackRate));
