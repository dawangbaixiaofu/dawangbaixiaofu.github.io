# Concepts


# design pattern
- observer
  > 创建了对象间的一种一对多的依赖关系，当一个对象状态改变时，所有依赖于它的对象都会得到通知并自动更新。
  
  signal
  
  ```py
  from time import sleep
  class Sprite:
      def __init__(self) -> None:
          self._is_processing = True
        
      def is_processing(self):
          return self._is_processing
      
      def set_processing(self, flag:bool):
          self._is_processing = flag
  
      
      def on_button_pressed(self):
          if self.is_processing():
              print("I am running.")
              self.set_processing(False)
          else:
              print("I am resting.")
              self.set_processing(True)
  
  
  class Button:
      def __init__(self, pressed:bool) -> None:
          self.pressed = pressed
    
      def signal(self, to: object, action_method:str):
          # to 是消息接收者, action 为接收者收到信息后的反应动作
          if self.pressed:
              reaction: callable = getattr(to, action_method)
              reaction() # 如果action有参数，在这里传递参数
  
  
  
  if __name__ == "__main__":
      sprite = Sprite()
      button = Button(pressed=True)
      while True:
          button.signal(sprite, 'on_button_pressed')
          sleep(1)
  
  ```
