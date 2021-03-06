```opengl
 #include <stdlib.h>
 #include <stdio.h>
 #include <GL/glut.h>
 
 //==========================================================================================//
 // Define
 //==========================================================================================//
 #ifndef KMYSKELTON
 #define KMYSKELTON
 
 #define KBOOL         int
 #define KTRUE           1
 #define KFALSE          0
 #define KWINDOW_W     480
 #define KWINDOW_H     480
 
 #endif // KMYSKELTON
 
 
 //==========================================================================================//
 // Globals
 //==========================================================================================//
 //---------------------------------------------------------------------------//
 // Status
 //---------------------------------------------------------------------------//
 extern KBOOL   GModeDebug         = KFALSE;
 extern int     GInterval          = 10;
 extern int     GIntervalCount     = 0;
 extern int     GFrameCount        = 0;
 extern int     GFPS               = 0;
 
 
 //---------------------------------------------------------------------------//
 // Light
 //---------------------------------------------------------------------------//
 extern GLfloat GLight0Position[] = {-10.0, 10.0, 5.0, 1.0};
 extern GLfloat GLight0Diffuse[]  = {1.0, 1.0, 1.0, 1.0};
 extern GLfloat GLight0Specular[] = {1.0, 1.0, 1.0, 1.0};
 extern GLfloat GLight0Off[]      = {0.0, 0.0, 0.0, 1.0}; 
 
 //---------------------------------------------------------------------------//
 // Light - Material
 //---------------------------------------------------------------------------//
 extern GLfloat GLightGreen[]     = {0.0f, 1.0f, 0.0f, 1.0f};
 extern GLfloat GDarkRed[]        = {0.8f, 0.1f, 0.1f, 1.0f};
 extern GLfloat GDimWhite[]       = {0.2f, 0.2f, 0.2f, 1.0f};
 extern GLfloat GShininess        = 20.0;
 
 //---------------------------------------------------------------------------//
 // Cube
 //---------------------------------------------------------------------------//
 extern GLfloat GCubeAngle = 0; 
 
 //---------------------------------------------------------------------------//
 // XYZ coordinate
 //---------------------------------------------------------------------------//
 extern GLdouble GXYZVertex[][3] = {
 	{ 0.0, 0.0, 0.0 },
 	{ 3.0, 0.0, 0.0 },
 	{ 0.0, 3.0, 0.0 },
 	{ 0.0, 0.0, 3.0 }
 };
 
 //==========================================================================================//
 // Functions
 //==========================================================================================//
 
 //---------------------------------------------------------------------------//
 // Draw Cube
 //---------------------------------------------------------------------------//
 void DrawCube(void) {
 	// Material & Lighting
 	glMaterialfv(GL_FRONT, GL_DIFFUSE, GLightGreen);
 	glMaterialfv(GL_FRONT, GL_SPECULAR, GDimWhite);
 	glMaterialf(GL_FRONT, GL_SHININESS, GShininess);
 
 	glPushMatrix(); 
 		glRotatef(GCubeAngle, 0.0, 1.0, 0.0); 
 		glutSolidCube(2.0); 
 		//glutSolidSphere(2.0, 10, 10);
 		//glutSolidTeapot(1);
 		//glutSolidCone(1.0, 3, 10, 10);
 	glPopMatrix(); 
 }
 
 //---------------------------------------------------------------------------//
 // Draw XYZ Coordinates
 //---------------------------------------------------------------------------//
 void DrawXYZ(void) {
 	glDisable(GL_LIGHTING);
 	glBegin(GL_LINES);
 		// X
 		glColor3f(1.0,0.0,0.0); // Red
 		glVertex3dv(GXYZVertex[0]);
 		glVertex3dv(GXYZVertex[1]);
 		// Y
 		glColor3f(0.0,1.0,0.0); // Green
 		glVertex3dv(GXYZVertex[0]);
 		glVertex3dv(GXYZVertex[2]); 
 		// Z
 		glColor3f(0.0,0.0,1.0); // Blue
 		glVertex3dv(GXYZVertex[0]);
 		glVertex3dv(GXYZVertex[3]); 
 	glEnd();
 	glEnable(GL_LIGHTING);
 }
 
 //---------------------------------------------------------------------------//
 // Main Display Callback function
 //---------------------------------------------------------------------------//
 void Display(void) {
 	glClear(GL_COLOR_BUFFER_BIT | GL_DEPTH_BUFFER_BIT);
 
 	DrawCube();
 
 	if (GModeDebug) {
 		DrawXYZ();
 	}
 	glutSwapBuffers();
 	glFlush();
 	GFrameCount++;
 }
 
 //---------------------------------------------------------------------------//
 // Idling Process
 //---------------------------------------------------------------------------//
 void Idle(void){
 	glutPostRedisplay(); 
 }
 
 //---------------------------------------------------------------------------//
 // Timer - Must be recursive
 //---------------------------------------------------------------------------//
 void Timer(int value) {	
 	// Stop timer if 0
 	if (value == 0) { return; }
 	
 	// Every GInterval mili sec update this
 	GCubeAngle = (GCubeAngle + 0.5); 
 	if(GCubeAngle > 360.0) {
 		GCubeAngle -= 0.0;
 	}
 	
 	// Calculate FPS
 	if ( (GIntervalCount * GInterval) > 1000) {
 		GFPS = GFrameCount;
 		GFrameCount = 0;
 		GIntervalCount=0;
 		if (GModeDebug == KTRUE) { printf("\rFPS = %d \r", GFPS); }
 	}
 	GIntervalCount++;
 	
 	glutPostRedisplay();
 	glutTimerFunc(GInterval, Timer, 1);
 }
 
 //---------------------------------------------------------------------------//
 // Keyboard Event Handler (Callback)
 //---------------------------------------------------------------------------//
 void Keyboard(unsigned char key, int x, int y) {
 	switch (key) {
 		// Exit
 		case 'q':
 		case 'Q':
 		case '\033':  // Esc
 			exit(0);
 		// Debug Display
 		case 'd':
 		case GLUT_KEY_F12:
 			if (GModeDebug) { GModeDebug = KFALSE; }
 			else { GModeDebug = KTRUE; }
 			break;
 		//case '\040':  // Space
 		default:
 			break;
 	}
 }
 //---------------------------------------------------------------------------//
 // Keyboard Event Handler for special keys(Callback)
 //---------------------------------------------------------------------------//
 void KeyboardSpecial(int key, int x, int y) {
 	switch (key) {
 		// Help Menu
 		case GLUT_KEY_F1:
 			break;
 		// Debug Display
 		case GLUT_KEY_F12:
 			if (GModeDebug) { GModeDebug = KFALSE; }
 			else { GModeDebug = KTRUE; }
 			break;
 		default:
 			break;
 	}
 }
 
 //---------------------------------------------------------------------------//
 // Mouse Event Handler (Callback)
 //---------------------------------------------------------------------------//
 void Mouse(int button, int state, int x, int y) {
 	switch (button) {
 		case GLUT_LEFT_BUTTON:
 			if (GModeDebug == KTRUE) { printf("left"); }
 		break;
 		case GLUT_MIDDLE_BUTTON:
 			if (GModeDebug == KTRUE) { printf("middle"); }
 		break;
 		case GLUT_RIGHT_BUTTON:
 			if (GModeDebug == KTRUE) { printf("right");	}
 		break;
 		default:
 		break;
 	}
 
 	switch (state) {
 		case GLUT_UP:
 			if (GModeDebug == KTRUE) { printf("up"); }
 		break;
 		case GLUT_DOWN:
 			if (GModeDebug == KTRUE) { printf("down"); }
 		break;
 		default:
 		break;
 	}
 
 	if (GModeDebug == KTRUE) { printf(" at (%d, %d)\n", x, y); }
 }
 
 
 //---------------------------------------------------------------------------//
 // Reshaping (This will call first time too)
 //---------------------------------------------------------------------------//
 void Reshape(GLsizei w, GLsizei h){
 	// Should be call when this is init
 	glViewport(0, 0, w, h);
 	glMatrixMode(GL_PROJECTION);
 	glLoadIdentity();
 	gluPerspective(60, (GLfloat)(w/h), 1.0, 20);
 	glMatrixMode(GL_MODELVIEW);
 	glLoadIdentity();
 	gluLookAt(
 		-5.0, 5.0, 5.0, 
 		0.0, 0.0, 0.0, 
 		0.0, 1.0, 0.0
 	);
 }
 
 
 //---------------------------------------------------------------------------//
 // Passive Motion Mouse Handler - x and y when button up
 //---------------------------------------------------------------------------//
 void PassiveMotion(int x, int y) {
 	if (GModeDebug == KTRUE) { printf("(%d, %d)\n", x, y); }
 }
 
 
 //---------------------------------------------------------------------------//
 // Initialization 
 //---------------------------------------------------------------------------//
 KBOOL Init(void) {
 	glShadeModel(GL_SMOOTH);
 	glEnable(GL_DEPTH_TEST);
 	glEnable(GL_LIGHTING);
 	glLightModelfv(GL_LIGHT_MODEL_AMBIENT, GLight0Off);
 	glLightModeli(GL_LIGHT_MODEL_LOCAL_VIEWER, GL_TRUE);
 	glLightfv(GL_LIGHT0, GL_POSITION, GLight0Position);
 	glLightfv(GL_LIGHT0, GL_DIFFUSE, GLight0Diffuse);
 	glLightfv(GL_LIGHT0, GL_SPECULAR, GLight0Specular);
 	glEnable(GL_LIGHT0);
 	glClearColor(0.2, 0.4, 0.5, 1.0);
 	return KTRUE;
 }
 
 //---------------------------------------------------------------------------//
 // Main Process 
 //---------------------------------------------------------------------------//
 int main(int argc, char **argv) {
 	// Initialization of window
 	glutInit(&argc, argv);
 	glutInitDisplayMode(GLUT_DOUBLE | GLUT_RGB | GLUT_DEPTH);
 	glutInitWindowSize(KWINDOW_W,KWINDOW_H);
 	glutCreateWindow("Cube");
 
 	// Callbacks
 	glutReshapeFunc(Reshape);
 	glutDisplayFunc(Display);
 	glutIdleFunc(Idle); 
 	glutKeyboardFunc(Keyboard);
 	glutSpecialFunc(KeyboardSpecial);
 	glutMouseFunc(Mouse);
 	glutPassiveMotionFunc(PassiveMotion);
 	glutTimerFunc(GInterval, Timer, 1);
 
 	// My Initialization
 	if (Init() == KFALSE) {
 		fprintf(stderr, "Failed to Init : %s (%d)\n", __FILE__, __LINE__);
 	}
 
 	glutMainLoop();
 	return 0;
 }
 //---------------------------------------------------------------------------//
 ```

