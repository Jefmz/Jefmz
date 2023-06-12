import turtle

# Configuração da janela do jogo
window = turtle.Screen()
window.title("Ping Pong")
window.bgcolor("black")
window.setup(width=800, height=600)
window.tracer(0)

# Paleta A
paleta_a = turtle.Turtle()
paleta_a.speed(0)
paleta_a.shape("square")
paleta_a.color("white")
paleta_a.shapesize(stretch_wid=6, stretch_len=1)
paleta_a.penup()
paleta_a.goto(-350, 0)

# Paleta B
paleta_b = turtle.Turtle()
paleta_b.speed(0)
paleta_b.shape("square")
paleta_b.color("white")
paleta_b.shapesize(stretch_wid=6, stretch_len=1)
paleta_b.penup()
paleta_b.goto(350, 0)

# Bola
bola = turtle.Turtle()
bola.speed(40)
bola.shape("circle")
bola.color("white")
bola.penup()
bola.goto(0, 0)
bola.dx = 0.2
bola.dy = 0.2

# Funções para movimentar as paletas
def paleta_a_up():
    y = paleta_a.ycor()
    if y < 250:
        y += 20
    paleta_a.sety(y)

def paleta_a_down():
    y = paleta_a.ycor()
    if y > -240:
        y -= 20
    paleta_a.sety(y)

def paleta_b_up():
    y = paleta_b.ycor()
    if y < 250:
        y += 20
    paleta_b.sety(y)

def paleta_b_down():
    y = paleta_b.ycor()
    if y > -240:
        y -= 20
    paleta_b.sety(y)

# Teclado
window.listen()
window.onkeypress(paleta_a_up, "w")
window.onkeypress(paleta_a_down, "s")
window.onkeypress(paleta_b_up, "Up")
window.onkeypress(paleta_b_down, "Down")

# Loop principal do jogo
while True:
    window.update()

    # Movimentação da bola
    bola.setx(bola.xcor() + bola.dx)
    bola.sety(bola.ycor() + bola.dy)

    # Colisão com as bordas
    if bola.ycor() > 290:
        bola.sety(290)
        bola.dy *= -1

    if bola.ycor() < -290:
        bola.sety(-290)
        bola.dy *= -1

    if bola.xcor() > 390:
        bola.goto(0, 0)
        bola.dx *= -1

    if bola.xcor() < -390:
        bola.goto(0, 0)
        bola.dx *= -1

    # Colisão com as paletas
    if (bola.dx > 0) and (350 > bola.xcor() > 340) and (paleta_b.ycor() + 50 > bola.ycor() > paleta_b.ycor() - 50):
        bola.setx(340)
        bola.dx *= -1

    if (bola.dx < 0) and (-350 < bola.xcor() < -340) and (paleta_a.ycor() + 50 > bola.ycor() > paleta_a.ycor() - 50):
        bola.setx(-340)
        bola.dx *= -1
