# gu2gl
A simple header redefinition &amp; utility library to translate sceGu styled code into OpenGL styled code

## Sample

```c
#define GUGL_IMPLEMENTATION
#include <gu2gl.h>

// ... boilerplate

int main(int argc, char* argv[])
{
	setupCallbacks();
        guglInit(list);
	int val = 0;

	while(running())
	{
                guglStartFrame(list, GL_FALSE);
	        glClearColor(0xff554433);
                glClearDepth(0);
                glClear(GL_COLOR_BUFFER_BIT | GL_DEPTH_BUFFER_BIT);
    
		glMatrixMode(GL_PROJECTION);
		glLoadIdentity();
		glPerspective(75.0f,16.0f/9.0f,0.5f,1000.0f);

		glMatrixMode(GL_VIEW);
		glLoadIdentity();

		glMatrixMode(GL_MODEL);
		glLoadIdentity();

		{
			ScePspFVector3 pos = { 0, 0, -2.5f };
			ScePspFVector3 rot = { val * 0.79f * (GL_PI/180.0f), val * 0.98f * (GL_PI/180.0f), val * 1.32f * (GL_PI/180.0f) };
			gluTranslate(&pos);
			gluRotateXYZ(&rot);
		}

		glDrawElements(GL_TRIANGLES,GL_TEXTURE_32BITF|GL_COLOR_8888|GL_VERTEX_32BITF|GL_TRANSFORM_3D,12*3,0,vertices);

                guglSwapBuffers(GL_TRUE, GL_FALSE);
		val++;
	}

        guglTerm();

	sceKernelExitGame();
	return 0;
}
```
