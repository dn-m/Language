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
measure = "#", [metrical-duration], [identifier-declaration];

(* Relationship *)
relationshipdeclaration = 
	identifier | identifier-group,
	whitespace, 
	relationship-operator, 
	whitespace,
	identifier | identifier-group,
	[identifier-declaration];

relationship-operator = 
	bidirectional-relationship-operator |
	immediate-unidirectional-relationship-operator |
	delayed-unidirectional-relationship-operator;

bidirectional-relationship-operator = "<>"
immediate-unidirectional-relationship-operator = "->"
delayed-unidirectional-relationship-operator = "~>" 
(* TODO: extend to specify delay by any time interval type *)

(* Metrical Duration *)
metrical-duration = int, ",", int;
(* e.g., 2,16 *)

metrical-duration-container = 
	metrical-duration, 
	[identifier, identifier], 
	[identifier-declaration];
(* e.g., 3,16 PerfID InstrID: EventID *)

(* Element *)
element = pitch; (* TODO: extend *)

(* Pitch *)
letter-name = 
	"a" | "b" | "c" | "d" | "e" | "f" | "g" | 
	"A" | "B" | "C" | "D" | "E" | "F" | "G";
quarter-step-modifier = "1/4" | "q" | "qtr" | "quarter";
sharp = "#" | "sharp";
flat = "b" | "flat";
half-step-modifier = sharp | flat;
eighth-step-up = "up";
eighth-step-down = "down";
eighth-step-modifier = eighth-step-up | eighth-step-down;
octave = digit;
named-pitch = 
	letter-name, 
	[([quarter-step-modifier] half-step-modifier)], 
	[eighth-step-modifier]
	[octave];

pitch = float | named-pitch;

```