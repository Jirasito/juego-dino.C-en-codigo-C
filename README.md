# juego-dino.C-en-codigo-C
#include <stdio.h>//Para funciones de entrada y salida estándar como printf.
#include <stdlib.h>// Para funciones generales como system (para limpiar la pantalla).
#include <conio.h>//Para funciones de manejo de teclado como _kbhit y _getch.
#include <windows.h>// Para la función Sleep, que nos permite pausar el juego."
//incluisiones y variables.
#define WIDTH 50
#define HEIGHT 10
#define JUMP_HEIGHT 5
#define GAME_SPEED 50
//variables globales
int gameOver;
int score;
int dinoX, dinoY;
int cactusX, cactusY;
//funcion setup
void setup() {
    gameOver = 0;
    score = 0;
    dinoX = 5;
    dinoY = HEIGHT - 1;
    cactusX = WIDTH - 5;
    cactusY = HEIGHT - 1;
}
//funcion draw
void draw() {
    system("cls");
    for (int i = 0; i < HEIGHT; i++) {
        for (int j = 0; j < WIDTH; j++) {
            if (i == dinoY && j == dinoX)
                printf("R");
            else if (i == cactusY && j == cactusX)
                printf("+");
            else if (i == HEIGHT - 1)
                printf("_");
            else
                printf(" ");
        }
        printf("\n");
    }
    printf("Score: %d\n", score);
}
//funcion jump
void jump() {
    if (dinoY >= HEIGHT - JUMP_HEIGHT)
        dinoY -= JUMP_HEIGHT;
}
//funcion input
void input() {
    if (_kbhit()) {   
        char key = _getch();
        if (key == ' ')
            jump();
    }
}
//funcion update
void update() {
    if (dinoY < HEIGHT - 1)
        dinoY++;
    cactusX--;
    if (cactusX <= 0) {
        cactusX = WIDTH - 5;
        score++;
    }
    if ((cactusX == dinoX) && (cactusY == dinoY))
        gameOver = 1;
}
//funcion main
int main() {
    setup();
    while (!gameOver) {
        draw();
        input();
        update();
        Sleep(GAME_SPEED);
    }
    printf("\nGame Over! Final Score: %d\n", score);
    return 0;
}
