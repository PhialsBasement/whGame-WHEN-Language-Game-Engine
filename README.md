# whGame Engine 🎮

A lightweight game engine written entirely in WHEN language, demonstrating the power and elegance of WHEN's conditional paradigm for game development.

## 🌟 Features

- **Pure WHEN Implementation** - No Python game code, just WHEN!
- **Sprite Management** - Create, move, and delete game sprites
- **Collision Detection** - Built-in AABB collision system
- **Keyboard Input** - Real-time keyboard event handling
- **Implicit Game Loop** - Leverages WHEN's main loop paradigm
- **Color Support** - Hex and named color support
- **Window Management** - Easy window creation and configuration

## 🚀 Quick Start

### Prerequisites

- [WHEN Language](https://github.com/YourUsername/WHEN-Language) interpreter installed
- Python 3.8+ (for the WHEN interpreter)
- tkinter (usually comes with Python)

### Installation

1. Clone this repository:
```bash
git clone https://github.com/YourUsername/whGame-Engine.git
cd whGame-Engine
```

2. Copy `whGame.when` to your WHEN project directory or ensure it's in the same directory as your game file.

### Your First Game

Create a file `my_game.when`:

```when
import whGame

player = None
player_x = 300
player_y = 300

main:
    # Initialize once
    when not whGame.initialized:
        whGame.init_engine(600, 400, "My First Game", "#000033")
        player = whGame.create_sprite(player_x, player_y, 40, 40, "#00FF00", "player")

    # Game loop
    when whGame.initialized and whGame.running:
        # Handle input
        when whGame.is_key_pressed("left"):
            player_x = player_x - 5
            whGame.move_sprite(player, -5, 0)

        when whGame.is_key_pressed("right"):
            player_x = player_x + 5
            whGame.move_sprite(player, 5, 0)

        # Update display
        whGame.update_display()
        sleep(0.016)  # 60 FPS

    # Exit on ESC
    when whGame.is_key_pressed("escape"):
        whGame.stop_game()
        exit()
```

Run your game:
```bash
python when.py my_game.when
```

## 📚 API Reference

### Initialization

#### `init_engine(width, height, title, bg_color)`
Initialize the game engine and create a window.
- `width`: Window width in pixels
- `height`: Window height in pixels
- `title`: Window title string
- `bg_color`: Background color (hex string or color name)

### Sprites

#### `create_sprite(x, y, width, height, color, tag)`
Create a new sprite.
- Returns: Sprite object with properties `x`, `y`, `width`, `height`, `color`, `tag`

#### `move_sprite(sprite, dx, dy)`
Move a sprite by delta values.

#### `set_sprite_position(sprite, x, y)`
Set absolute position of a sprite.

#### `delete_sprite(sprite)`
Remove a sprite from the game.

### Input

#### `is_key_pressed(key)`
Check if a key is currently pressed.
- Common keys: `"left"`, `"right"`, `"up"`, `"down"`, `"space"`, `"escape"`, `"a"`-`"z"`, `"0"`-`"9"`

### Collision

#### `check_collision(sprite1, sprite2)`
Check if two sprites are colliding using AABB detection.
- Returns: `True` if colliding, `False` otherwise

#### `on_collision(tag1, tag2, handler_function)`
Register a collision handler for sprites with specific tags.
- `handler_function`: Called with `(sprite1, sprite2)` when collision occurs

### Display

#### `update_display()`
Refresh the game display. Call this each frame.

#### `draw_text(x, y, text, color, font)`
Draw text on screen.
- `font`: Optional tuple like `("Arial", 20)`

#### `clear_canvas()`
Clear all sprites from the display.

### Game Control

#### `stop_game()`
Stop the game loop and close the window.

#### Properties
- `whGame.initialized`: Boolean, true after init_engine
- `whGame.running`: Boolean, true while game is active
- `whGame.window_width`: Current window width
- `whGame.window_height`: Current window height

## 🎮 Example Games

### Asteroid Blaster
A classic space shooter where you defend against falling asteroids.
```bash
python when.py examples_asteroid.when
```

**Controls:**
- Arrow Keys: Move left/right
- Space: Fire bullets
- ESC: Exit

### Space Shooter
A vertical scrolling shooter with enemy waves.
```bash
python when.py examples_space.when
```

**Controls:**
- Arrow Keys: Move left/right
- Space: Shoot
- ESC: Exit

## 🏗️ Architecture

whGame leverages WHEN language's unique features:

### Implicit Game Loop
```when
main:
    when whGame.initialized and whGame.running:
        # This runs every frame automatically!
        update_game()
        whGame.update_display()
```

### Conditional Game Logic
```when
# No if/else needed!
when player.health <= 0:
    game_over = True

when game_over:
    display_game_over_screen()

when not game_over:
    continue_gameplay()
```

### Error-Free Collision Handling
```when
# Using WHEN's safe_call for robust collision detection
collision_result = safe_call(whGame.check_collision, player, enemy)

when is_success(collision_result) and get_result(collision_result):
    handle_player_hit()
```

## 🔧 Advanced Features

### Custom Collision Handlers
```when
def on_bullet_hits_enemy(bullet, enemy):
    score = score + 10
    whGame.delete_sprite(bullet)
    whGame.delete_sprite(enemy)

whGame.on_collision("bullet", "enemy", on_bullet_hits_enemy)
```

### Sprite Velocity System
```when
# Set sprite velocity
whGame.set_sprite_velocity(enemy, 0, 2)  # Move down at 2 pixels/frame

# Update all sprites with velocity
whGame.update_all_sprites_physics()
```

### Game State Management
```when
game_state = "menu"

main:
    when game_state == "menu":
        show_menu()
        when whGame.is_key_pressed("space"):
            game_state = "playing"

    when game_state == "playing":
        run_game()
        when player_lives == 0:
            game_state = "game_over"

    when game_state == "game_over":
        show_game_over()
        when whGame.is_key_pressed("r"):
            reset_game()
            game_state = "menu"
```

## 🤝 Contributing

We welcome contributions! whGame is a demonstration of WHEN language capabilities, and we'd love to see what you can build with it.

### Ideas for Contributions:
- New example games
- Additional sprite shapes (circles, polygons)
- Particle systems
- Sound support (if WHEN adds audio capabilities)
- Animation system
- Tilemap support

## 📝 License

MIT License - feel free to use whGame in your own projects!

## 🙏 Acknowledgments

- Built for the [WHEN Language](https://github.com/YourUsername/WHEN-Language)
- Inspired by classic game engines but reimagined in WHEN's unique paradigm
- Thanks to the WHEN community for testing and feedback

## 🐛 Known Limitations

- No audio support (WHEN language limitation)
- Basic shapes only (rectangles)
- No image/sprite sheet support (WHEN uses colored rectangles)
- Single window only
- No fullscreen mode

## 🚦 Roadmap

- [ ] Sprite rotation
- [ ] Particle effects system
- [ ] Multiple collision shapes
- [ ] Scene management
- [ ] Save/Load game state
- [ ] Networking support for multiplayer
- [ ] Performance optimizations
- [ ] Mobile touch input support

---

**Made with ❤️ in WHEN Language**

*Remember: In WHEN, everything is a condition, even your game loop!*