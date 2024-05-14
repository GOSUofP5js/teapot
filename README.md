# teapot




## CODE

    #include <windows.h>
    #include <gl/glut.h>
    
    float angleX = 0.0f; // x축 회전 각도
    float angleY = 0.0f; // y축 회전 각도
    
    void display() {
        glClear(GL_COLOR_BUFFER_BIT | GL_DEPTH_BUFFER_BIT);
        
        glLoadIdentity(); // 변환 매트릭스 초기화
        glTranslatef(0, 0, 0); // 주전자를 시야 안쪽으로 이동
        glRotatef(angleX, 1.0f, 0.0f, 0.0f); // x축 주위로 회전
        glRotatef(angleY, 0.0f, 1.0f, 0.0f); // y축 주위로 회전
        
        glutWireTeapot(0.5); // 주전자 그리기
        glutSwapBuffers();
    }
    
    void init() {
        glClearColor(0.0, 0.0, 0.0, 0.0);
        glMatrixMode(GL_PROJECTION);
        glLoadIdentity();
        glOrtho(-1.0, 1.0, -1.0, 1.0, -1.0, 1.0);
        glMatrixMode(GL_MODELVIEW);
        glLoadIdentity();
        glEnable(GL_DEPTH_TEST);
    }
    
    void timer(int value) {
        angleX += 1.0f; // 매번 1도씩 x축 회전
        angleY += 1.0f; // 매번 1도씩 y축 회전
        glutPostRedisplay(); // 화면 갱신 요청
        glutTimerFunc(16, timer, 0); // 60fps로 설정
    }
    
    int main(int argc, char** argv) {
        glutInit(&argc, argv);
        glutInitDisplayMode(GLUT_DOUBLE | GLUT_RGB | GLUT_DEPTH);
        glutInitWindowSize(500, 500);
        glutCreateWindow("Teapot");
        glutDisplayFunc(display);
        init();
        glutTimerFunc(0, timer, 0); // 타이머 설정
        glutMainLoop();
        return 0;
    }

