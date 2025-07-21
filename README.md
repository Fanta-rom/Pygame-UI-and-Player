# Pygame-UI-and-Player

This is a simple UI and Player Class I made for my coding class and i thought it would help out others that are getting started with pygame, because I had a hard time with the Ui because it didnt have any widgets.

# Example Usage:

NOTE:
this is example code, I didnt check if it works, but it should clarify any confusion about how to use the modules accordingly, it also contains a few print(interaction) for debugging, so you can know what caused the crash.

Setup:
Pygame:
```py
  import pygame
  import sys # optional. only if you want the program to terminate ASAP, as shown in the loop below
  
  pygame.init()
  pygame.font.init()
  pygame.mixer.init()
  Font = pygame.font.Font(size = 50)
  screen = pygame.display.set_mode((width, height), pygame.FULLSCREEN | pygame.SCALED)
  clock = pygame.time.Clock()
```
  Buttons:
```py
    PlayButton = Button("Play", DARK_GREY, 20, 100, 170, 50,
                        text_color=YELLOW, rounded=True)
    OptionsButton = Button("Options", DARK_GREY, 20, 165, 170,50,
                           text_color=YELLOW, rounded=True)
    CreditsButton = Button("Credits", DARK_GREY, 20, 230, 170, 50,
                           text_color=YELLOW, rounded=True)
    QuitButton = Button("Quit", DARK_GREY, 20, 295, 170, 50,
                        text_color=YELLOW, rounded=True)
```             
  Text:
```py
    OverlayText = Text("",0,0,Font,YELLOW)
```  
  Radio Buttons:
```py
    RB1 = RadioButton("RED",250,120,20,BLACK,WHITE,WHITE,True,Font)
    RB2 = RadioButton("BLUE",250,170,20,BLACK,WHITE,WHITE,False,Font)
    RB3 = RadioButton("GREEN",250,220,20,BLACK,WHITE,WHITE,False,Font)
    RB4 = RadioButton("YELLOW",250,270,20,BLACK,WHITE,WHITE,False,Font)
    RB5 = RadioButton("ORANGE",500,120,20,BLACK,WHITE,WHITE,False,Font)
    RB6 = RadioButton("BLACK",500,170,20,BLACK,WHITE,WHITE,False,Font)
    RB7 = RadioButton("WHITE",500,220,20,BLACK,WHITE,WHITE,False,Font)
    ColorGroup = RadioGroup()
    ColorGroup.add(RB1)
    ColorGroup.add(RB2)
    ColorGroup.add(RB3)
    ColorGroup.add(RB4)
    ColorGroup.add(RB5)
    ColorGroup.add(RB6)
    ColorGroup.add(RB7)
```
  Check Box:
```py
    ThemeCHK = CheckBox("Tune",130,170,30,BLACK,WHITE,WHITE,False,Font)
```
  Slider:
```py
    VolumeSlider = Slider(screen, 220, 120, 300, 20, min=0, max=100, initial=100, step=1)
```
Ui (examples):
```py
  def mainmenu():
      if not pygame.mixer.music.get_busy():
          pygame.mixer.music.load("D:/Asus/WAV player lol/.venv/Lib/Music/elevate.wav")
          pygame.mixer.music.play(-1)
      if selectedtheme == 0:
          PlayButton.update_rect_color(BLACK)
          OptionsButton.update_rect_color(BLACK)
          QuitButton.update_rect_color(BLACK)
          NamePlate.update_text_color(WHITE)
          PlayButton.update_text_color(WHITE)
          OptionsButton.update_text_color(WHITE)
          QuitButton.update_text_color(WHITE)
      elif selectedtheme == 1:
          PlayButton.update_rect_color(WHITE)
          OptionsButton.update_rect_color(WHITE)
          QuitButton.update_rect_color(WHITE)
          NamePlate.update_text_color(BLACK)
          PlayButton.update_text_color(BLACK)
          OptionsButton.update_text_color(BLACK)
          QuitButton.update_text_color(BLACK)
      elif selectedtheme == 2:
          PlayButton.update_rect_color(GREY)
          OptionsButton.update_rect_color(GREY)
          QuitButton.update_rect_color(GREY)
          NamePlate.update_text_color(WHITE)
          PlayButton.update_text_color(WHITE)
          OptionsButton.update_text_color(WHITE)
          QuitButton.update_text_color(WHITE)
      NamePlate.draw(screen)
      PlayButton.draw(screen)
      OptionsButton.draw(screen)
      QuitButton.draw(screen)
  
  def options():
      screen.fill(GREY)
      OverlayText.x = 300
      OverlayText.y = 10
      OverlayText.update_text("Options")
      OverlayText.draw(screen)
      BackButton.draw(screen)
      VolumeSlider.listen(pygame.event.get())
      OverlayText.x = 10
      OverlayText.y = 120
      OverlayText.update_text("Volume")
      OverlayText.draw(screen)
      VolumeSlider.draw()
      OverlayText.y = 240
      OverlayText.update_text("Theme")
      OverlayText.draw(screen)
      ColorGroup.draw(screen)
```
Loop:
```py
  current_screen = "menu"
  running = True
  while running:
      # logic
      events = pygame.event.get()
      VolumeSlider.listen(events)
      for event in events:
          if current_screen=="options":
              ColorGroup.handle_event(event) 
          if event.type == pygame.QUIT:
              sys.exit() # or pygame.quit() if you dont need the sys library
          elif PlayButton.is_clicked(event) and current_screen == "menu":
              print("Play button clicked!")
              current_screen = "play"
          elif OptionsButton.is_clicked(event) and current_screen == "menu":
              print("Options button clicked!")
              current_screen = "options"
          elif QuitButton.is_clicked(event) and current_screen == "menu":
              print("Quit button clicked!")
              sys.exit() # or pygame.quit() if you dont need the sys library

        volume = VolumeSlider.getValue() / 100
        pygame.mixer.music.set_volume(volume)
        
        keys = pygame.key.get_pressed()
          if current_screen == "options" and (
                  (event.type == pygame.KEYDOWN and event.key == pygame.K_ESCAPE) or BackButton.is_clicked(event)):
              print("Exiting options menu...")
              current_screen = "menu"
          elif current_screen == "play" and (
                  (event.type == pygame.KEYDOWN and event.key == pygame.K_ESCAPE) or BackButton.is_clicked(event)):
              print("Exiting play menu...")
              current_screen = "menu"

    if current_screen == "menu":
        mainmenu()
    elif current_screen == "options":
      options()
    pygame.display.flip() # Refresh the screen
      clock.tick(100) # 100 FPS 
```
