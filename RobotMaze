#include "library.h"
 image * pacman = image_from_file("pacman.bmp");
 image * wincoin = image_from_file("wincoin.bmp");
 image * start = image_from_file("start.bmp");
 image * robot = image_from_file("robot.bmp");
 image * robot2 = image_from_file("robot2.bmp");

 struct location{
	 int row;
	 int column;
 };
 int steps;

 int maze_rows, maze_columns, startx, starty, pxpos, pypos, ex, ey, startex, startey,e2x, e2y, starte2x, starte2y;

 location win;

 location maze[100000];
 location mazetraveled[100000];
 location prevlocation[100000];
 location eprevlocation[100000];
 location eprevlocationall[100000];
 location prevlocationall[100000];

 int read_file(){
	 ifstream fin;
	 fin.open("maze.txt");
	 if (fin.fail()) {
		 cerr << "failed to open file " << "maze.txt" << endl;
		 return -1;
	 }
	 string line_data;
	 string column[10000];
	 int i = 0;
	 while (!fin.eof()){
		 getline(fin, line_data);
		 column[i] = line_data;
		 maze_rows = line_data.length();
		 i++;
	 }
	 maze_columns = i;
 }


 int read_maze(){
	 ifstream fin;
	 fin.open("maze.txt");
	 if (fin.fail()) {
		 cerr << "failed to open file " << "maze.txt" << endl;
		 return -1;
	 }
	 int b = 0;
	 int num = 0;
	 bool enemy1 = false, enemy2 = false;
	 int erandom, e2random;
	 while (b < maze_columns){
		 char maze_data;
		 for (int i = 0; i < maze_rows; i++){
			 fin >> maze_data;
			 set_pen_color(color::black);
			 fill_rectangle(i * 20, b * 20, 20, 20);
			 if (enemy1 == false){
				erandom = random_in_range(0, 40);
			 }
			 if (enemy2 == false){
				 e2random = random_in_range(0, 40);
			 }
			 if (maze_data == '+'){
				 maze[num].row = 0;
				 maze[num].column = 0;
				 set_pen_color(color::green);
				 startx = i;
				 starty = b;
			 }
			 else if (maze_data == '$'){
				 maze[num].row = 1;
				 maze[num].column = 1;
				 win.row = i;
				 win.column = b;
				 set_pen_color(color::red);
			 }
			 else if (maze_data == '#'){
				 maze[num].row = 2;
				 maze[num].column = 2;
				 set_pen_color(color::grey);
			 }
			 else if (maze_data == '~'){
				 maze[num].row = 3;
				 maze[num].column = 3;
				 set_pen_color(color::white);
				 if (erandom == 5 && enemy1 == false){
					 ex = i;
					 startex = i;
					 ey = b;
					 startey = b;
					 enemy1 = true;
				 }
				 if (e2random == 5 && enemy2 == false){
					 e2x = i;
					 starte2x = i;
					 e2y = b;
					 starte2y = b;
					 enemy2 = true;
				 }
			 }
			// else if (maze_data == 'E'){
			//	 maze[num].row = 3;
			//	 maze[num].column = 3;
			//	 set_pen_color(color::white);
			//	 ex = i;
			//	 startex = i;
			//	 ey = b;
			//	 startey = b;
			// }
			 fill_rectangle(i * 20 + 1, b * 20 + 1, 20 - 2, 20 - 2);
			 num++;
		 }
		 b++;
	 }
	 fin.close();
	 return 0;
 }

 int draw_maze(){
	 read_maze();
	 int b = 0;
	 int num = 0;
	 while (b < maze_columns){
		 for (int i = 0; i < maze_rows; i++){
			 set_pen_color(color::black);
			 fill_rectangle(i * 20, b * 20, 20, 20);
			 if (maze[num].row == 0){
				 set_pen_color(color::green);
				 draw_image(wincoin, i * 20 + 1, b * 20 + 1);
			 }
			 else if (maze[num].row == 1){
				 set_pen_color(color::red);
				 draw_image(wincoin, i * 20 + 1, b * 20 + 1);
			 }
			 else if (maze[num].row == 2){
				 set_pen_color(color::grey);
				 fill_rectangle(i * 20 + 1, b * 20 + 1, 20 - 2, 20 - 2);
			 }
			 else if (maze[num].row == 3){
				 set_pen_color(color::white);
				 fill_rectangle(i * 20 + 1, b * 20 + 1, 20 - 2, 20 - 2);
			 }
			 num++;
		 }
		 b++;
	 }
	 return 0;
 }

 int yellowBrickRoad(){
	 int b = 0;
	 int num = 0;
	 while (b < steps){
		 int x = prevlocation[b].row;
		int  y = prevlocation[b].column;
		set_pen_color(color::yellow);
		fill_rectangle(x * 20 + 1, y * 20 + 1, 20 - 2, 20 - 2);
		 b++;
	 }
	 return 0;
 }

 void game(){
	 int x = startx;
	 int y = starty;
	 int ex = startex;
	 int ey = startey;
	 bool automatic = false;
	 bool end = false;
	 bool on = true;
	 int j = 0, l = 0;
	 int p = 0, t, u = 0;
	// set_pen_color(color::purple);
	// fill_rectangle(x * 20 + 1, y * 20 + 1, 20 - 2, 20 - 2);
	 draw_image(pacman, x * 20 + 1, y * 20 + 1);
	// set_pen_color(color::cyan);
	// fill_rectangle(ex * 20 + 1, ey * 20 + 1, 20 - 2, 20 - 2);
	 draw_image(robot, ex * 20 + 1, ey * 20 + 1);
	 draw_image(robot2, e2x * 20 + 1, e2y * 20 + 1);
	 while (on = true){
		 while (automatic == false)
		 {
			 int num = ((y)* maze_rows) + x;
			 char c = wait_for_key_typed();
			 if (c == 'n') automatic = true;
			 if (maze[num].row == 0){
				 draw_image(start, x * 20 + 1, y * 20 + 1);
			 }
			 else if (maze[num].row == 1){
				 draw_image(wincoin, x * 20 + 1, y * 20 + 1);
			 }
			 else if (maze[num].row == 2){
				 set_pen_color(color::grey);
				 fill_rectangle(x * 20 + 1, y * 20 + 1, 20 - 2, 20 - 2);
			 }
			 else if (maze[num].row == 3){
				 set_pen_color(color::white);
				 fill_rectangle(x * 20 + 1, y * 20 + 1, 20 - 2, 20 - 2);
			 }
			 if (c == 'w')
			 {
				 prevlocation[j].row = x;
				 prevlocation[j].column = y;
				 prevlocationall[l].row = x;
				 prevlocationall[l].column = y;
				 j++;
				 l++;
				 y--;
				 if (maze[((y)* maze_rows) + x].row == 2){
					 y++;
				 }
			 }
			 else if (c == 'a')
			 {
				 prevlocation[j].row = x;
				 prevlocation[j].column = y;
				 prevlocationall[l].row = x;
				 prevlocationall[l].column = y;
				 j++;
				 l++;
				 x--;
				 if (maze[((y)* maze_rows) + x].row == 2){
					 x++;
				 }
			 }
			 else if (c == 's')
			 {
				 prevlocation[j].row = x;
				 prevlocation[j].column = y;
				 prevlocationall[l].row = x;
				 prevlocationall[l].column = y;
				 j++;
				 l++;
				 y++;
				 if (maze[((y)* maze_rows) + x].row == 2){
					 y--;
				 }
			 }
			 else if (c == 'd')
			 {
				 prevlocation[j].row = x;
				 prevlocation[j].column = y;
				 prevlocationall[l].row = x;
				 prevlocationall[l].column = y;
				 j++;
				 l++;
				 x++;
				 if (maze[((y)* maze_rows) + x].row == 2){
					 x--;
				 }
			 }
			 else if (c == 'b' && j > 0)
			 {
				 x = prevlocation[j-1].row;
				 y = prevlocation[j-1].column;
				 prevlocationall[l].row = x;
				 prevlocationall[l].column = y;
				 l++;
				 j--;
			 }
			// set_pen_color(color::purple);
			// fill_rectangle(x * 20 + 1, y * 20 + 1, 20 - 2, 20 - 2);
			 draw_image(pacman, x * 20 + 1, y * 20 + 1);
			 int r = 0;
			 bool up = true, left = true, right = true, down = true, back = false;
			 num = ((ey)* maze_rows) + ex;
			 c = wait_for_key_typed(0.0);
			 if (p == 0){
				 t = p;
			 }
			 if (p != 0){
				 t = p - 1;
			 }
			 for (t; t >= 0; t--){
				 //	 if (l == 0) right = true;
				 if (eprevlocationall[t].column == ey - 1 && ex == eprevlocationall[t].row || maze[((ey - 1)* maze_rows) + ex].row == 2) up = false;
				 if (eprevlocationall[t].column == ey  && ex - 1 == eprevlocationall[t].row || maze[((ey)* maze_rows) + (ex - 1)].row == 2) left = false;
				 if (eprevlocationall[t].column == ey + 1 && ex == eprevlocationall[t].row || maze[((ey + 1)* maze_rows) + ex].row == 2) down = false;
				 if (eprevlocationall[t].column == ey  && ex + 1 == eprevlocationall[t].row || maze[((ey)* maze_rows) + (ex + 1)].row == 2) right = false;
				 if (t == 0) back = true;
			 }
			 if (p == 0) r = 4;
			 else if (up == true) r = 1;
			 else if (left == true) r = 2;
			 else if (down == true) r = 3;
			 else  if (right == true) r = 4;
			 else if (back == true) r = 5;
			 if (c == 'm') automatic = false;
			 if (maze[num].row == 0){
				 set_pen_color(color::green);
				 draw_image(start, ex * 20 + 1, ey * 20 + 1);
			 }
			 else if (maze[num].row == 1){
				 set_pen_color(color::red);
				 draw_image(wincoin, ex * 20 + 1, ey * 20 + 1);
			 }
			 else if (maze[num].row == 2){
				 set_pen_color(color::grey);
				 fill_rectangle(ex * 20 + 1, ey * 20 + 1, 20 - 2, 20 - 2);

			 }
			 else if (maze[num].row == 3){
				 set_pen_color(color::white);
				 fill_rectangle(ex * 20 + 1, ey * 20 + 1, 20 - 2, 20 - 2);

			 }
			 if (r == 1)
			 {
				 eprevlocation[u].row = ex;
				 eprevlocation[u].column = ey;
				 eprevlocationall[l].row = ex;
				 eprevlocationall[l].column = ey;
				 p++;
				 u++;
				 ey--;
				 if (maze[((ey)* maze_rows) + ex].row == 2){
					 ey++;
				 }
			 }
			 else if (r == 2)
			 {
				 eprevlocation[u].row = ex;
				 eprevlocation[u].column = ey;
				 eprevlocationall[l].row = ex;
				 eprevlocationall[l].column = ey;
				 p++;
				 u++;
				 ex--;
				 if (maze[((ey)* maze_rows) + ex].row == 2){
					 ex++;
				 }
			 }
			 else if (r == 3)
			 {
				 eprevlocation[u].row = ex;
				 eprevlocation[u].column = ey;
				 eprevlocationall[l].row = ex;
				 eprevlocationall[l].column = ey;
				 p++;
				 u++;
				 ey++;
				 if (maze[((ey)* maze_rows) + ex].row == 2){
					 ey--;
				 }
			 }
			 else if (r == 4)
			 {
				 eprevlocation[u].row = ex;
				 eprevlocation[u].column = ey;
				 eprevlocationall[l].row = ex;
				 eprevlocationall[l].column = ey;
				 p++;
				 u++;
				 ex++;
				 if (maze[((ey)* maze_rows) + ex].row == 2){
					 ex--;
				 }
			 }
			 else if (r == 5 && u>0)
			 {
				 eprevlocationall[p].row = ex;
				 eprevlocationall[p].column = ey;
				 ex = eprevlocation[u - 1].row;
				 ey = eprevlocation[u - 1].column;

				 p++;
				 u--;
			 }
			// set_pen_color(color::cyan);
			// fill_rectangle(ex * 20 + 1, ey * 20 + 1, 20 - 2, 20 - 2);

			 num = ((e2y)* maze_rows) + e2x;
			 c = wait_for_key_typed(0.0);
			  r = random_in_range(1, 4);
			 if (c == 'n') automatic = true;
			 if (maze[num].row == 0){
				 set_pen_color(color::green);
				 draw_image(start, e2x * 20 + 1, e2y * 20 + 1);
			 }
			 else if (maze[num].row == 1){
				 set_pen_color(color::red);
				 draw_image(wincoin, e2x * 20 + 1, e2y * 20 + 1);
			 }
			 else if (maze[num].row == 2){
				 set_pen_color(color::grey);
				 fill_rectangle(e2x * 20 + 1, e2y * 20 + 1, 20 - 2, 20 - 2);
			 }
			 else if (maze[num].row == 3){
				 set_pen_color(color::white);
				 fill_rectangle(e2x * 20 + 1, e2y * 20 + 1, 20 - 2, 20 - 2);
			 }
			
			 if (r == 1)
			 {
				 e2y--;
				 if (maze[((e2y)* maze_rows) + e2x].row == 2){
					 e2y++;
				 }
			 }
			 else if (r == 2)
			 {
				 e2x--;
				 if (maze[((e2y)* maze_rows) + e2x].row == 2){
					 e2x++;
				 }
			 }
			 else if (r == 3)
			 {
				 e2y++;
				 if (maze[((e2y)* maze_rows) + e2x].row == 2){
					 e2y--;
				 }
			 }
			 else if (r == 4)
			 {
				 e2x++;
				 if (maze[((e2y)* maze_rows) + e2x].row == 2){
					 e2x--;
				 }
			 }
			 draw_image(robot2, e2x * 20 + 1, e2y * 20 + 1);
			 draw_image(robot, ex * 20 + 1, ey * 20 + 1);
			 draw_image(pacman, x * 20 + 1, y * 20 + 1);
			 if (ex == x && ey == y || e2x == x && e2y == y) {
				 move_to((maze_rows * 20) / 2, (maze_columns * 20) / 2);
				 set_font_size(50);
				 steps = j;
				 yellowBrickRoad();
				 set_pen_color(color::black);
				 write_string("game over");
			
				 return;
			 }
			 if (win.row == x && win.column == y) {
				 move_to((maze_rows * 20) / 2, (maze_columns * 20) / 2);
				 set_font_size(50);
				 steps = j;
				 yellowBrickRoad();
				 set_pen_color(color::black);
				 write_string("you win!!!");
			
				 return;
			 }
		 }
		 while (automatic == true)
		 {
			 int num = ((y)* maze_rows) + x;
			 int r =0;
			 bool up = true, left = true, right = true, down = true, back = false;
			 char c = wait_for_key_typed(0.0);
			 int k;
			 if (l == 0){
				 k = l;
			 }
			 if (l != 0){
				 k = l-1;
			 }
			 for (k; k >= 0; k--){
			//	 if (l == 0) right = true;
				 if (prevlocationall[k].column == y - 1 && x == prevlocationall[k].row || maze[((y-1)* maze_rows) + x].row ==2) up = false;
				  if (prevlocationall[k].column == y  && x - 1 == prevlocationall[k].row || maze[((y)* maze_rows) + (x-1)].row == 2) left = false;
				  if (prevlocationall[k].column == y + 1 && x == prevlocationall[k].row ||maze[((y + 1)* maze_rows) + x].row ==2) down = false;
				  if (prevlocationall[k].column == y  && x + 1 == prevlocationall[k].row || maze[((y)* maze_rows) + (x+1)].row ==2) right = false;
				  if (k==0) back = true;
			 }
			 if (l == 0) r = 4;
			 else if (up == true) r = 1;
			 else if (left == true) r = 2;
			 else if (down == true) r = 3;
			 else  if (right == true) r = 4;
			 else if (back == true) r = 5;
			 wait(0.01);
			 if (c == 'm') automatic = false;
			 if (maze[num].row == 0){
				 set_pen_color(color::green);
				 draw_image(start, x * 20 + 1, y * 20 + 1);
			 }
			 else if (maze[num].row == 1){
				 set_pen_color(color::red);
				 draw_image(wincoin, x * 20 + 1, y * 20 + 1);
			 }
			 else if (maze[num].row == 2){
				 set_pen_color(color::grey);
				 fill_rectangle(x * 20 + 1, y * 20 + 1, 20 - 2, 20 - 2);

			 }
			 else if (maze[num].row == 3){
				 set_pen_color(color::white);
				 fill_rectangle(x * 20 + 1, y * 20 + 1, 20 - 2, 20 - 2);

			 }
			 if (r ==1)
			 {
				 prevlocation[j].row = x;
				 prevlocation[j].column = y;
				 prevlocationall[l].row = x;
				 prevlocationall[l].column = y;
				 l++;
				 j++;
				 y--;
				 if (maze[((y)* maze_rows) + x].row == 2){
					 y++;
				 }
			 }
			 else if (r == 2)
			 {
				 prevlocation[j].row = x;
				 prevlocation[j].column = y;
				 prevlocationall[l].row = x;
				 prevlocationall[l].column = y;
				 l++;
				 j++;
				 x--;
				 if (maze[((y)* maze_rows) + x].row == 2){
					 x++;
				 }
			 }
			 else if (r == 3)
			 {
				 prevlocation[j].row = x;
				 prevlocation[j].column = y;
				 prevlocationall[l].row = x;
				 prevlocationall[l].column = y;
				 l++;
				 j++;
				 y++;
				 if (maze[((y)* maze_rows) + x].row == 2){
					 y--;
				 }
			 }
			 else if (r == 4)
			 {
				 prevlocation[j].row = x;
				 prevlocation[j].column = y;
				 prevlocationall[l].row = x;
				 prevlocationall[l].column = y;
				 l++;
				 j++;
				 x++;
				 if (maze[((y)* maze_rows) + x].row == 2){
					 x--;
				 }
			 }
			 else if (r == 5 && j>0)
			 {
				 prevlocationall[l].row = x;
				 prevlocationall[l].column = y;
				 x = prevlocation[j - 1].row;
				 y = prevlocation[j - 1].column;
			
				 l++;
				 j--;
			 }
			// set_pen_color(color::purple);
			// fill_rectangle(x * 20 + 1, y * 20 + 1, 20 - 2, 20 - 2);
			 draw_image(pacman, x * 20 + 1, y * 20 + 1);
			  r = 0;
			 up = true, left = true, right = true, down = true, back = false;
			 num = ((ey)* maze_rows) + ex;
			 c = wait_for_key_typed(0.0);
			 if (p == 0){
				 t = p;
			 }
			 if (p != 0){
				 t = p - 1;
			 }
			 for (t; t >= 0; t--){
				 //	 if (l == 0) right = true;
				 if (eprevlocationall[t].column == ey - 1 && ex == eprevlocationall[t].row || maze[((ey - 1)* maze_rows) + ex].row == 2) up = false;
				 if (eprevlocationall[t].column == ey  && ex - 1 == eprevlocationall[t].row || maze[((ey)* maze_rows) + (ex - 1)].row == 2) left = false;
				 if (eprevlocationall[t].column == ey + 1 && ex == eprevlocationall[t].row || maze[((ey + 1)* maze_rows) + ex].row == 2) down = false;
				 if (eprevlocationall[t].column == ey  && ex + 1 == eprevlocationall[t].row || maze[((ey)* maze_rows) + (ex + 1)].row == 2) right = false;
				 if (t == 0) back = true;
			 }
			 if (p == 0) r = 4;
			 else if (up == true) r = 1;
			 else if (left == true) r = 2;
			 else if (down == true) r = 3;
			 else  if (right == true) r = 4;
			 else if (back == true) r = 5;
			 if (c == 'm') automatic = false;
			 if (maze[num].row == 0){
				 set_pen_color(color::green);
				 draw_image(start, ex * 20 + 1, ey * 20 + 1);
			 }
			 else if (maze[num].row == 1){
				 set_pen_color(color::red);
				 draw_image(wincoin, ex * 20 + 1, ey * 20 + 1);
			 }
			 else if (maze[num].row == 2){
				 set_pen_color(color::grey);
				 fill_rectangle(ex * 20 + 1,ey * 20 + 1, 20 - 2, 20 - 2);

			 }
			 else if (maze[num].row == 3){
				 set_pen_color(color::white);
				 fill_rectangle(ex * 20 + 1, ey * 20 + 1, 20 - 2, 20 - 2);

			 }
			 if (r == 1)
			 {
				 eprevlocation[u].row = ex;
				 eprevlocation[u].column = ey;
				 eprevlocationall[l].row = ex;
				 eprevlocationall[l].column = ey;
				 p++;
				 u++;
				 ey--;
				 if (maze[((ey)* maze_rows) + ex].row == 2){
					 ey++;
				 }
			 }
			 else if (r == 2)
			 {
				 eprevlocation[u].row = ex;
				 eprevlocation[u].column = ey;
				 eprevlocationall[l].row = ex;
				 eprevlocationall[l].column = ey;
				 p++;
				 u++;
				 ex--;
				 if (maze[((ey)* maze_rows) + ex].row == 2){
					 ex++;
				 }
			 }
			 else if (r == 3)
			 {
				 eprevlocation[u].row = ex;
				 eprevlocation[u].column = ey;
				 eprevlocationall[l].row = ex;
				 eprevlocationall[l].column = ey;
				 p++;
				 u++;
				 ey++;
				 if (maze[((ey)* maze_rows) + ex].row == 2){
					 ey--;
				 }
			 }
			 else if (r == 4)
			 {
				 eprevlocation[u].row = ex;
				 eprevlocation[u].column = ey;
				 eprevlocationall[l].row = ex;
				 eprevlocationall[l].column = ey;
				 p++;
				 u++;
				 ex++;
				 if (maze[((ey)* maze_rows) + ex].row == 2){
					 ex--;
				 }
			 }
			 else if (r == 5 && u>0)
			 {
				 eprevlocationall[p].row = ex;
				 eprevlocationall[p].column = ey;
				 ex = eprevlocation[u - 1].row;
				 ey = eprevlocation[u - 1].column;

				 p++;
				 u--;
			 }
			// set_pen_color(color::cyan);
			// fill_rectangle(ex * 20 + 1, ey * 20 + 1, 20 - 2, 20 - 2);
			 num = ((e2y)* maze_rows) + e2x;
			 c = wait_for_key_typed(0.0);
			  r = random_in_range(1, 4);
			 if (c == 'n') automatic = true;
			 if (maze[num].row == 0){
				 set_pen_color(color::green);
				 draw_image(start, e2x * 20 + 1, e2y * 20 + 1);
			 }
			 else if (maze[num].row == 1){
				 set_pen_color(color::red);
				 draw_image(wincoin, e2x * 20 + 1, e2y * 20 + 1);
			 }
			 else if (maze[num].row == 2){
				 set_pen_color(color::grey);
				 fill_rectangle(e2x * 20 + 1, e2y * 20 + 1, 20 - 2, 20 - 2);
			 }
			 else if (maze[num].row == 3){
				 set_pen_color(color::white);
				 fill_rectangle(e2x * 20 + 1, e2y * 20 + 1, 20 - 2, 20 - 2);
			 }
			 if (r == 1)
			 {
				 e2y--;
				 if (maze[((e2y)* maze_rows) + e2x].row == 2){
					 e2y++;
				 }
			 }
			 else if (r == 2)
			 {
				 e2x--;
				 if (maze[((e2y)* maze_rows) + e2x].row == 2){
					 e2x++;
				 }
			 }
			 else if (r == 3)
			 {
				 e2y++;
				 if (maze[((e2y)* maze_rows) + e2x].row == 2){
					 e2y--;
				 }
			 }
			 else if (r == 4)
			 {
				 e2x++;
				 if (maze[((e2y)* maze_rows) + e2x].row == 2){
					 e2x--;
				 }
			 }
			 draw_image(robot2, e2x * 20 + 1, e2y * 20 + 1);
			 draw_image(robot, ex * 20 + 1, ey * 20 + 1);
			 draw_image(pacman, x * 20 + 1, y * 20 + 1);
			 if (ex == x && ey == y || e2x == x && e2y == y) {
				 move_to((maze_rows * 20) / 2, (maze_columns * 20) / 2);
				 set_font_size(50);
				 steps = j;
				 yellowBrickRoad();
				set_pen_color(color::black);
				 write_string("game over");
				
				 on = false;
				 return;
			 }
			 if (win.row == x && win.column == y) {
				 move_to((maze_rows * 20) / 2, (maze_columns * 20) / 2);
				 set_font_size(50);
				 steps = j;
				 yellowBrickRoad();
				 set_pen_color(color::black);
				 write_string("you win!!");
			
				 on = false;
				 return;
			 }
		 }
	 }
 }

 void new_game(){
	 cout << "do you want to start a new game? (y/n)" << endl;
	 char answer = wait_for_key_typed();
	 if (answer == 'y') {
		 clear();
		 draw_maze();
		 game();
	 }
	 if (answer == 'n') {
		 clear();
		 exit();
	 }
 }

 void main(){
	 read_file();
	 cout << "pacman is your character, your goal is to get from the start sign to the coin" << endl << "without touching the enemy blue or red ghosts" <<
		 endl << "keys to move are w,a,s,d" << endl << "press N for automatic, and M for manual, and B to move back" << endl;
	 make_window(maze_rows * 20, maze_columns * 20);
	 read_maze();
	 draw_maze();
	 game();
	 while (true){
		 new_game();
	 }
 }
