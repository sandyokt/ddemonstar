#include <iostream>
#include <GL/glew.h>
#include <GL/glut.h>
#include <GL/GL.h>
#include <corona.h>
#include <Windows.h>

int width = 400, height = 480, spritePos = 0, spriteLocation, spriteLocation2;
bool keys[255], press;
float spriteWidth = 24, spriteHeight = 24.5;
GLuint texture[2];

void renderBitmapString(float x, float y, float z, void *font, char *string)
{
	glBindTexture(GL_TEXTURE_2D, 0);
	char *c;
	glRasterPos3f(x, y, z);
	for (c = string; *c != '\0'; c++)
	{
		glutBitmapCharacter(font, *c);
	}
}

void loadTexture(char filename[], int pos) {
	corona::Image *image = corona::OpenImage(filename);

	glGenTextures(1, &texture[pos]);
	glBindTexture(GL_TEXTURE_2D, texture[pos]);

	glTexParameteri(GL_TEXTURE_2D, GL_TEXTURE_MAG_FILTER, GL_NEAREST);
	glTexParameteri(GL_TEXTURE_2D, GL_TEXTURE_MIN_FILTER, GL_NEAREST);
	glTexImage2D(GL_TEXTURE_2D, 0, GL_RGBA, image->getWidth(), image->getHeight(), 0, GL_RGBA, GL_UNSIGNED_BYTE, image->getPixels());
}


void display() {
	
	glClear(GL_COLOR_BUFFER_BIT | GL_DEPTH_BUFFER_BIT);
	loadTexture("Assets/bgMenu.png", 0);

	glEnable(GL_TEXTURE_2D);
	glBindTexture(GL_TEXTURE_2D, texture[0]);

	glBegin(GL_QUADS);
	glTexCoord2f(0, 1); glVertex3i(0, 0, 0);
	glTexCoord2f(1, 1); glVertex3i(width, 0, 0);
	glTexCoord2f(1, 0); glVertex3i(width, height, 0);
	glTexCoord2f(0, 0); glVertex3i(0, height, 0);
	glEnd();

	glEnable(GL_TEXTURE_2D);
	glBindTexture(GL_TEXTURE_2D, texture[1]);

	renderBitmapString(150, 420, 0, GLUT_BITMAP_HELVETICA_18, "DDemonstar");
	renderBitmapString(90, 150, 0, GLUT_BITMAP_HELVETICA_18, "Press Enter to Start Game");
	renderBitmapString(60, 130, 0, GLUT_BITMAP_HELVETICA_10, "How to Play : Press [W/A/S/D] Key to Move, and [ESC] to");
	renderBitmapString(150, 110, 0, GLUT_BITMAP_HELVETICA_10, "Back to Main Menu");
	renderBitmapString(10, 10, 0, GLUT_BITMAP_HELVETICA_10, "High Score : 200");
	renderBitmapString(320, 10, 0, GLUT_BITMAP_HELVETICA_10, "Sound(M) : On");

	glutSwapBuffers();

}

void keyboard(unsigned char key, int x, int y) {
	if (key == 'a') {
		spritePos--;
		spriteLocation -= 10;
	}
	else if (key == 'd') {
		spritePos++;
		spriteLocation += 10;
	}
	else if (key == 'w') {
		spriteLocation2 += 10;
	}
	else if (key == 's') {
		spriteLocation2 -= 10;
	}
	else if (key == 27) {
		glutDisplayFunc(display);
	}
	if (spritePos < 0) {
		spritePos = 17;
	}
	else if (spritePos > 17) {
		spritePos = 0;
	}
	glutPostRedisplay();
}

void displaygame() {

	glClear(GL_COLOR_BUFFER_BIT | GL_DEPTH_BUFFER_BIT);
	loadTexture("Assets/bg.png", 0);

	glEnable(GL_TEXTURE_2D);
	glBindTexture(GL_TEXTURE_2D, texture[0]);

	glBegin(GL_QUADS);
	glTexCoord2f(0, 1); glVertex3i(0, 0, 0);
	glTexCoord2f(1, 1); glVertex3i(width, 0, 0);
	glTexCoord2f(1, 0); glVertex3i(width, height, 0);
	glTexCoord2f(0, 0); glVertex3i(0, height, 0);
	glEnd();

	glEnable(GL_BLEND);
	glBlendFunc(GL_SRC_ALPHA, GL_ONE_MINUS_SRC_ALPHA);
	loadTexture("Assets/ships.png", 1);

	glEnable(GL_TEXTURE_2D);
	glBindTexture(GL_TEXTURE_2D, texture[1]);
	
	glBegin(GL_QUADS);
	glTexCoord2f(spriteWidth * spritePos / 407.9, spriteHeight/ 48);		glVertex3i(170 + spriteLocation, 50 + spriteLocation2, 0);
	glTexCoord2f(spriteWidth * (spritePos+1) / 407.9, spriteHeight / 48);	glVertex3i(220 + spriteLocation, 50 + spriteLocation2, 0);
	glTexCoord2f(spriteWidth * (spritePos + 1) / 407.9, 0);					glVertex3i(220 + spriteLocation, 100 + spriteLocation2, 0);
	glTexCoord2f(spriteWidth * spritePos / 407.9, 0);						glVertex3i(170 + spriteLocation, 100 + spriteLocation2, 0);
	glEnd();

	renderBitmapString(260, 9, 0, GLUT_BITMAP_HELVETICA_12, "Wave : 1 Lv : 1 HP : 15");
	glutKeyboardFunc(keyboard);
	glutSwapBuffers();

}

void keyboardawal(unsigned char key, int x, int y) {
	printf("Normal key: %d\n", key);
	if (press)
	{
		keys[key] = true;
	}
	else if (press)
	{
		keys[key] = false;
	}
	if (key == 13) {
		glutDisplayFunc(displaygame);
	}
	
	glutPostRedisplay();
}

int main(int argc, char **args) {
	glutInit(&argc, args);
	glutInitDisplayMode(GLUT_RGBA | GLUT_DOUBLE);
	glutInitWindowSize(400, 480);
	glutCreateWindow("DDmonstar");
	glutDisplayFunc(display);
	glutKeyboardFunc(keyboardawal);

	
	

	
	glMatrixMode(GL_PROJECTION);
	glOrtho(0, width, 0, height, 0, -1);
	glMatrixMode(GL_MODELVIEW);

	glutMainLoop();

}
