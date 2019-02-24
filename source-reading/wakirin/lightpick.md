Repository:    	https://github.com/mitsuhiko/indicatif
Description:   	Javascript date range picker - lightweight, no jQuery
Commit:        	564037b
Main Language: 	Javascript 
Dependencies:	momentjs

The relationship between source files:
.
├── lightpick.js
└── css
    └── lightpick.css

* lightpick.js:
This is the main file of the library, defining all of the function and logic.
The file is following UMD template.
- private variable default: defining default options.
- private methods: renderCalendar(), renderTopButtons(), renderMonthsOfYear(), renderDay()...
- public Lightpick as a prototype class base and providing public methods.

* lightpick.css:
This is all css styles of the library.