```

(* General *)
whitespace = " ", "\t" (* others... *);
letter = "a" | ... | "z" | "A" | ... | "Z";
digit = "0" | nonzerodigit;
nonzerodigit = "1" | "2" | "3" | "4" | "5" | "6" | "7" | "8" | "9"; 
zero = "0";
natural-number = { digit };
int = ["-"], natural-number;
float = ["-"], natural-number , ".", natural-number;
identifier = letter, { letter | digit | "_" };
identifier-declaration = ":", whitespace, identifier;
identifier-group = "(", identifier, {",", identifier}, ")";

(* Structure *)
section = "$", [identifier-declaration];
measure = "#", [metricalduration], [identifier-declaration];

(* Relationship *)
relationshipdeclaration = 
	identifier | identifier-group,
	whitespace, 
	relationshipoperator, 
	whitespace,
	identifier | identifier-group,
	[identifier-declaration];

relationshipoperator = 
	bidirectionalrelationshipoperator |
	immediateunidirectionalrelationshipoperator |
	delayedunidirectionalrelationshipoperator;

bidirectionalrelationshipoperator = "<>"
immediateunidirectionalrelationshipoperator = "->"
delayedunidirectionalrelationshipoperator = "~>" 
(* TODO: extend to specify delay by any time interval type *)

(* Metrical Duration *)
metricalduration = int, ",", int;
(* e.g., 2,16 *)

metricaldurationcontainer = 
	metricalduration, 
	[identifier, identifier], 
	[identifier-declaration];
(* e.g., 3,16 PerfID InstrID: EventID *)

(* Element *)
element = pitch; (* TODO: extend *)

(* Pitch *)
lettername = 
	"a" | "b" | "c" | "d" | "e" | "f" | "g" | 
	"A" | "B" | "C" | "D" | "E" | "F" | "G";
quarterstepmodifier = "1/4" | "q" | "qtr" | "quarter";
sharp = "#" | "sharp";
flat = "b" | "flat";
halfstepindicator = sharp | flat;
eighthstepup = "up";
eighthstepdown = "down";
eighthstepmodifier = eighthstepup | eighthstepdown;
octave = digit;
namedpitch = 
	lettername, 
	[([quarterstepmodifier] halfstepindicator)], 
	[eighthstepmodifier]
	[octave];

pitch = float | namedpitch;

```