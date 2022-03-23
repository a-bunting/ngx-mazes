# NgxMazes

The library is designed to help angular developers create perfect mazes easily with a graph as scaffolding for movement within the maze.

This library was generated with [Angular CLI](https://github.com/angular/angular-cli) version 13.2.0.

## Add to Project

To add this to your Angular project is simple. Fromn the terminal in your project run `npm install ngx-mazes`, and then in the component you want to use it create an object by `const maze: MazeAlgorithms = new PrimsMaze()` where PrimsMaze may be the name of any algorithm genration method. 

## Usage

Creating a maze is fairly straightforward and certain helper functions are included to allow easily changes to the mazes.

`
    // start by creating a new maze object. This is what will provide the functionality for the maze.
    let maze: MazeAlgorithms = new AldousBroderMaze();

    let widthOfMaze: number = 50;
    let heightOfMaze: number = 25;

    // all data which is poured out of the algorithms is done so via an observable. This is because mazes can either be built over time (to show the maze being generated) or instantly.
    this.mazedata = maze.currentData.subscribe((data: IterationData) => {
        // get the actual maze structure from data.maze
        this.maze = data.maze;
        // this next step will create a mirror of the maze in the Y direction with one opening between the two halves.
        this.maze = maze.mirrorMazeYDirection(data.maze, 1);
        // this next step will create a mirror of the maze in the X direction with two openings between the two halves.
        this.maze = maze.mirrorMazeXDirection(this.maze, 2);
        // this next function makes the walls thicker, so it looks a bit cooler or provides no sharp turns (for games)
        this.maze = maze.makeWallsThick(data.maze);
        // the final function adds a room in the middle of the maze, this can also add rooms at any point around the maze. No doors are provided and need to be manually removed for now.
        this.maze = maze.addRoom(this.maze);
        // finally generate a graph of the maze, which will be useful if you need some sort of traversal of the maze, such as if you plan on implementing A* aqlgoritms to plot routes.
        this.mazeGraph = maze.generateMazeGraph(this.maze);
    })

    // generate the maze object
    maze.generateMaze(widthOfMaze, heightOfMaze);
  }`
