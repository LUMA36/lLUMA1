extends CharacterBody2D

# Hareket Hızı
var speed = 300
# Saldırı Gücü
var attack_power = 10
# Saldırı Mesafesi
var attack_range = 50
a
func _physics_process(delta):
    var velocity = Vector2.ZERO

    # Hareket
    if Input.is_action_pressed("ui_right"):
        velocity.x += 1
    if Input.is_action_pressed("ui_left"):
        velocity.x -= 1
    if Input.is_action_pressed("ui_down"):
        velocity.y += 1
    if Input.is_action_pressed("ui_up"):
        velocity.y -= 1

    velocity = velocity.normalized() * speed
    move_and_slide(velocity)

    # Saldırı
    if Input.is_action_just_pressed("attack"):
        attack()

func attack():
    # Düşmanları tespit et
    var enemies = get_parent().get_children()
    for e in enemies:
        if e.is_in_group("enemies") and position.distance_to(e.position) < attack_range:
            e.take_damage(attack_power)
            
