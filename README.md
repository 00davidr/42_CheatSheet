# 42 School Cheat Sheet by [Antonin Gavrel](www.github.com/agavrel)

*Intended for 42 current and future 42 students*

### Introduction to 42

Description from the US School official website:
> 42 is more than just a disruptive educational model and coding school. What makes us unique and a major player in the tech world are the defining characteristics of the 42 culture. Every element of 42 shows our culture, from the students, to the curriculum structure and content, to the $0 tuition and innovative admissions process.

Most of the course are about C coding.

### About the "Piscine"
The piscine is the entrance exam that consists of 4 weeks fully dedicated at solving exercises and submitting group and solo projects.  
Although the school advise you to "come as you are", and this is what I did, it does certainly help to prepare beforehand.  
You can find the [subject on github](https://github.com/Binary-Hackers/42_Subjects/tree/master/01_Piscines/C/EN), courtesy of my friend binary hacker.
As this cheatsheet is intended for 42 students I will not talk too much about this. Few things to know:

**Guidelines to succeed:**
* It does not matter if you fail a project, an exam or a day as long as you keep striving. Someone who has never been interested before in Computer Science would never be able to complete everything in time, yet he will not prevent from being successful.
* My opinion on what are the criteria to succeed are: 1/ How far you went on the 4 exams session, knowing that the 3 firsts exams are limited in term of how far you can go, 2/ to have an acceptable percentage of review from peers (probably 80% is enough, but you would get 90 to 97% if you are nice). 3/ The logging time has no or very little influence, but it certainly directly influence your skills, 4/ it is strongly advised to succeed at least one group project.
* There is a special and unique achievement awarded to the most helpful/smart student. This achievement does not show up on the student profile until he asks for it.

### 42 Projects Guides
|Name|Track|Hashtags|What you will learn|
|-|-|-|-|
|Fillit|General|Architecture, Parsing, Algo|[Description from a student](https://medium.com/@bethnenniger/fillit-solving-for-the-smallest-square-of-tetrominos-c6316004f909)|
|Printf|Algorithm|Architecture, Parsing, utf-8|[UTF-8 Conversion table](https://en.wikipedia.org/wiki/UTF-8)<br>[Variadic Function](https://en.wikipedia.org/wiki/Variadic_function)|
|Filler|Algorithm|Parsing, Algo, Bot|42 forums have good threads on this project|
|Lem-In|Algorithm|Parsing, Algo, Chained-Lists|[Dijkstra's algorithm](https://en.wikipedia.org/wiki/Dijkstra%27s_algorithm)|
|Corewar|Algorithm|Architecture, parsing, disassembler, virus, VM|[About the original Game](https://en.wikipedia.org/wiki/Core_War)|
|LS|System|Parsing, Recursion, Chained-Lists|[The Good Old Manual](http://man7.org/linux/man-pages/man1/ls.1.html)|
|Minishell|System|Environment Variables, Shell|[Bourne Shell](https://en.wikipedia.org/wiki/Bourne_shell)|
|Malloc|System|Algo, Memory, HashCollision|[The Good Old Manual](http://man7.org/linux/man-pages/man3/malloc.3.html)|
|FDF|Infographics|Parsing, Creativity|[Bresenham's line algorithm](https://en.wikipedia.org/wiki/Bresenham%27s_line_algorithm), [Use of Graphics Library](https://en.wikipedia.org/wiki/Graphics_library), [Trigonometry](https://en.wikipedia.org/wiki/Trigonometry), [Rotations](https://en.wikipedia.org/wiki/Rotation_(mathematics)), [3D Projection](https://en.wikipedia.org/wiki/3D_projection), [ARGB Color Space](https://en.wikipedia.org/wiki/RGBA_color_space)|
|Fractol|Infographics|Fractals, Mathematics, ARGB, HUV|[Mandelbrot Set](https://en.wikipedia.org/wiki/Mandelbrot_set)|
|Wolfenstein 3d|Infographics|Raytracing, Rotation|[About the original Wolfenstein 3d](https://en.wikipedia.org/wiki/Wolfenstein_3D)|

**How to choose your specialization**
There are currently 4 main branches: [Infographics](https://en.wikipedia.org/wiki/Infographic), Algorithms, System and Web.
All branchs are interesting and you should try to explore each branch's initial project:
* If you are aiming to work in the video game industry then you should go for Infographics. Remember that this path is tough and not necessarily as rewarding as the other ones, but you will have the luxury to work in the video game industry.
* The Algorithm branch gradation is/was mainly based on flawless parsing and not so much on algorithm quality. Fortunately with the nomination of Benny as the head of the Pedagogy there will be more efforts to reward smart algorithms. Algorithms is the best one if you want to join a prestigious company like Google
* System is the best for those who like security, network and how computers truly work since you will have to ultimately recode your own operating system.
* Web is good for those who like to build websites, perhaps mobile app as well (react native) and want to become a freelancer.


### C Must-Read Books
*Download if you are a petty thief like me, adding the "torrent" or "pdf" keyword behind:*

The C Programming Language *by Brian Kernighan and Dennis Ritchie*  
[[C++] Optimizing software in C++ - Agner Fog (pdf)](https://www.agner.org/optimize/optimizing_cpp.pdf)  

### Common Beginner Mistakes

#### Array overflow
C does not perform boundary checking when using arrays.  
If you access outside the bounds of a stack based array it will just access another part of already allocated stack space, like in this example:

```c
void    somefunction3(void)
{
    int a[5];

    printf("%d\n", a[5]); // as 5 it is a size of the array and you try to access it it will overflow. Remember that the maximum array index you can ever access is its size minus 1.
}
```

#### Segmentation Fault
Many potential reasons for this.

##### A/ Loop segfault
One commonly reason is that you declared a loop and either 1/ forgot to increment the counter or 2/ forgot the exit condition:
```c
int i = 0;

while (i < 10)
{
    {some stuff}
    // but where is i++ ?
}
```

```c
int somevariable = 0;
while (42) // always true
{
    {some stuff}
    if (somevariable == 1) // make sure that somevariable will equal 1 at some point.
        break ;
}
```

Correct way:
```c
int i = 0;

while (i < 10)
{
    {some stuff}
    i++;
}
```

*Practice: what about this loop ?*
```c
unsigned char c = 0;

while (c < 150)
{
    {some stuff}
    c++;
}
```

##### B/ Accessing the next link in a chained-list without checking the current one
Another example with linked-lists
```c
typedef struct  s_list {
      void      *data;
      t_list    *next;
 }              t_list;

/*
** function to go 2 links further in a chained-list
*/

void somefunction(t_list *list)
{
    if (list->next != NULL)
    {
        list = list->next->next;
    }
}
```

if the current link of list is null you will get a segfault. The correct way is to always check the current link before the next one:

```c
void somefunction(t_list *list)
{
    if (list && list->next) // if both list and list->next exist
    {
        list = list->next->next;
    }
}
```

##### C/ Accessing an index in a loop for program with either graphics or a board game
```c
int somefunction(int y_max, int x_max, int array[y_max][x_max]);
{
    int y;
    int x;

    y  = 0;
    while (y < y_max)
    {
        x = 0;
        while (x < x_max)
        {
            if (array[y][x-1] > array[y][x]) // don't you see there is a problem ?
            {
                array[y][x] = array[y][x-1];
            }
            if (array[y+1][x] > array[y][x]) // don't you see there is another problem ?
            {
                array[y][x] = array[y+1][x];
            }
        }

    }
}
```

These lines should be corrected the following way:
```c
if (x > 0 && array[y][x-1] > array[y][x])
if (y < y_max - 1 && array[y+1][x] > array[y][x]) // strictly inferior to last possible index which is y_max - 1,
// you may also write y <= y_max - 2
```

You may also notice that we can even do better by changing the starting value of x or the exit condition of the y loop **in the case that we were to check only one of the two if conditions.**
```c
x = 1;
while (y < y_max - 1)
```


#### Accessing value of a local variable
Local variable value are allocated on the stack, which is cleaned once you exit the function.
```c
void increment_a(int a)
{
    a++; // it will have no effect
}

int solve(void)
{
    int a = 5;

    increment_a(a);
}
```

Hence if you want to modify a value you either have to use a pointer to the memory address:
```c
void increment_a(int *a)
{
    *a++;
}

int solve(void)
{
    int a = 5;

    increment_a(&a);
}
```

or return the local value:
```c
int increment_a(int a)
{
    return a+1;
}

int solve(void)
{
    int a = 5;

    a = increment_a(a);
}
```

#### Unprotected malloc
Do NOT leave a malloc unprotected:
```c
int allocate_memory(void)
{
    int *matrix;

    matrix = malloc(sizeof(int) * 9))

    return matrix;
}

int somefunction(void)
{
    int *matrix;

    matrix = allocate_memory();
}
```

Protect both the malloc **and its return value**:
It is not good enough to protect the malloc in the callee function (the function called) if the returned value is not also protected in the caller function (the function 'above')
```c
int allocate_memory(void)
{
    int *matrix;

    if (!(matrix = malloc(sizeof(int) * 9))) // this is short for matrix = malloc(sizeof(int) * 9; if (matrix == NULL)
		return NULL;   // the malloc is now protected,

    return matrix;
}

int somefunction(void)
{
    int *matrix;

    if ((matrix = allocate_memory()) == NULL) // the return value is also protected
        exit(); // note that often you can't or don't want to use exit() and will need to return 0 along all the functions up to the main function.
}
```

#### Freeing memory that has already been fred

Following the previous example, if you don't need the variable matrix anymore you can free it just by using:
```c
free(matrix); // do not attempt to free twice or to free a stack based variable
```

```c
free(matrix); // do not attempt to free twice or to free a stack based variable
```

##### Do Not use global variables
Global variables are forbidden in 42 School except for a few exceptions, see this interesting article: [Are Global Variables Bad](https://stackoverflow.com/questions/484635/are-global-variables-bad)
However many students, me including, found a way to circumvent this interdiction: you first declare a structure in the header that will contain all our variables:
```c
typedef struct s_env
{
    int a;
    int b;
    int c[4];
    // ... other variables you may need
}           t_env;
```
And then using it the following way in the program:
```c
void somefunction2(t_env *env)
{
    env->b = 2;
}

void somefunction(t_env *env)
{
    env->a = 1;

    somefunction2(env);
}

int main(void)
{
    t_env env;

    somefunction(&env);

    printf("%d\n", env.a);
    printf("%d\n", env.b);
}
```

This is "legal" in 42 (it is not a global variable, it is a structure passed along functions), it "works", but it is a very poor architecture choice. It is okay for beginner to do this but as your skill grows you should find more clever ways to architecture your programs.

#### VLA - Variable Length Arrays
The following example is a VLA and this is bad for many reasons, the most critical being that the memory is allocated on the stack which has a limited size.
```c
int somefunction(int y, int x, int array[y][x]);
```
[Waiter! There's a VLA in my C!](http://ayekat.ch/blog/vla)

#### using ft_ prefix for all functions

*ft_* is intended for functions you want to add to the libft project and use along your projects, not for specific program functions.

---
### Good practices

Now some guidelines that should hopefully help your coding style

#### Using structure for basic items

If you are using coordinates it might be interesting to create a structure 'point' or 'coord'

```
typedef struct s_point
{
    int y;
    int x;
}           t_point;

void somefunction(void){
    t_point p;

    p.x = 2;
    p.y = 5;

    //alternatively:  p = {5, 2};
}
```

#### Naming conventions

I once met a developer who was using hp and mp instead of x and y for coordinates.  
It was surely funny, original and a very good reference to JRPG... but it was not suitable name.  
The function name should always be:
* In English, forget about chauvinism!
* At least 5 letters. It is okay to have shorter exceptionally for well-known variables like int index -> int i, temporary -> tmp and pointer -> ptr.
* Self-explanatory: build_graph instead of graph or build_it
* For long name use either camel case (saveClientConfig) or snake case (save_client_config) and stick to one style.

#### Using flag for projects' options
For each project you will often have to parse flag input. In Linux the flag usually come after a '-' and allow for extra functionalities.
It is quite useful know how you can store such critical information into only 4 bytes *which is sizeof(integer)*
```c
static int	ft_strchr_index(char *s, int c)
{
	int		i;

	i = 0;
	while (s[i])
	{
		if (s[i] == c)
			return (i);
		++i;
	}
	return (-1);
}

int			get_flags(char *s, int *flags)
{
	int		n;

	while (*(++s))
	{
		if ((n = ft_strchr_index("alRrtdG1Ss", *s)) == -1)
			return (0);
		*flags |= (1 << n);
	}
	return (1);
}

int			main(int ac, char **av)
{
	int	i;

	int flags = 0;
	i = 0;
	while (++i < ac && av[i][0] == '-' && av[i][1])
	{
		if (av[i][1] == '-' && av[i][2])
			return (i + 1);
		if (!get_flags(av[i], &flags))
			return (-1);
	}
	return (i);
}
```

The a flag will be on bit 1, l on bit 2, R on bit 4, r on bit 8 etc.
You can then test if the flag was on by using the following:
```c
#define FLAG_A  0b001
#define FLAG_L  0b010
#define FLAG_RR 0b100
#include <stdio.h>

void    somefunction(int *flags)
{
    if (flags & FLAG_A)
        printf("Flag a is set!\n");    
}
```

You can unset a flag by clearing the corresponding bit the following way:
```c
void    somefunction2(int *flags)
{
    flags &= ~FLAG_A;
}
```

##### Using gcc flags for Makefile
```
gcc -Wall -Wextra -Werror -O2
```
* O2 will improve performance  ##Create a new repository on the command line
* pedantic is not requested but is a good one to check ISO C compliance

> Issue all the warnings demanded by strict ISO C and ISO C++; reject all programs that use forbidden extensions, and some other programs that do not follow ISO C and ISO C++. For ISO C, follows the version of the ISO C standard specified by any -std option used.


You can read the details about each flag on [gccgnu website](https://gcc.gnu.org/onlinedocs/gcc/Warning-Options.html)

#### Using preprocessor DEBUG macros

You can improve the performance of your program by using what we call preprocessor macros

# define DEBUG true


#### Setting up a new Git Repository using CLI (command line interface)

It can be done easily using the following command line:  
```
reponame='docker'
mkdir $reponame
touch README.md
git init
git add README.md
git commit -m "[INIT] First commit"
git remote add origin git@github.com:agavrel/$reponame.git
git push -u origin master
```

#### [Run Commands in Background](https://linuxize.com/post/how-to-run-linux-commands-in-background/) (could be used to recompile automatically each time .c are saved)

You can have multiple processes running in the background at the same time with ```&``` after the command.  
However the background process will continue to write messages to the terminal from which you invoked the command.  

To suppress the stdout and stderr messages use the following syntax:  
```
command > /dev/null 2>&1 &
```

```>/dev/null 2>&1``` means redirect ```stdout``` to ```/dev/null``` and ```stderr``` to ```stdout```

Use the jobs utility to display the status of all stopped and background jobs in the current shell session:
```
jobs -l
```
_NB: a Job is the process running thanks to the command execution_

To bring the job to the foreground use :
```
fg %ID
```
NB: you can use ```bg``` to do the reverse, from foreground to background.

To kill the process use:
```
kill -9 ID
```
Obviously replace ```ID``` in the above examples with the job ID you got from ```jobs -l```.
