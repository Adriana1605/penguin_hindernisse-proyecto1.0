# penguin_hindernisse-proyecto1.0
Juego
El juego lleva por nombre penguin hindernisse es un juego donde un pinguino tiene que atravesar las plataformas para poder llegar a la pratafomra para llegar al siguiente nivel.

Jugador 
extends CharacterBody2D

var velocidad = 200
var brinco = -400
var gravedad = 1000
# Variables para el sistema de puntos
var puntaje = 0
var vida = 3  # Asumiendo que empieza con 3 vidas
@onready var label_puntaje = $LabelPuntaje  # Asegúrate de tener un nodo Label en tu escena

func _ready():
	add_to_group("jugador")
	
# moviento Basicos del (jugador) , ( moverse de i, D, Saltar,etc)
func _physics_process(delta):
	var direccion = Input.get_axis("ui_left","ui_right")
	velocity.x = direccion * velocidad
	
	if not is_on_floor():
		velocity.y += gravedad * delta
	
	if Input.is_action_just_pressed("ui_up") and is_on_floor():
		velocity.y = brinco
	move_and_slide()

# --- Sistema de puntos y Label ---
func sumar_puntos(cantidad : int):
	puntaje += cantidad
	

func guardar_datos():
	var datos = {
		"jugador": {
			"puntaje": puntaje,
			"vida": vida,
			"posicion": {
				"x": "%.8f" % global_position.x,
				"y": "%.8f" % global_position.y
			}			
		}
	}

	
# Reiniciar (jugador)
@warning_ignore("unused_parameter")
func _on_reset_area_body_entered(body: Node2D) -> void:
	get_tree().reload_current_scene()

@warning_ignore("unused_parameter")
func _on_reset_area_2_body_entered(body: Node2D) -> void:
	get_tree().reload_current_scene()

func _on_reset_area_3_body_entered(body: Node2D) -> void:
	get_tree().reload_current_scene()

# portales ( Siguiente Nivel )
@warning_ignore("unused_parameter")
func _on_Portal_body_entered(body: Node2D) -> void:
	get_tree().change_scene_to_file("res://Level1.tscn")

func _on_portal1_body_entered(body: Node2D) -> void:
	get_tree().change_scene_to_file("res://Level2.tscn")

func _on_portal_2_body_exited(body: Node2D) -> void:
	get_tree().change_scene_to_file("res://Level0.tscn")
 
Activos del juego
Personaje:




