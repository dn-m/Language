(* General *)
whitespace = " ", "\t" (* others... *);
letter = "a" | ... | "z" | "A" | ... | "Z";
digit = "0" | nonzerodigit;
nonzerodigit = "1" | "2" | "3" | "4" | "5" | "6" | "7" | "8" | "9"; 
zero = "0";
naturalnumber = nonzerodigit, { digit };
int = ["-"], naturalnumber;
float = ["-"], { naturalnumber } , ".", { naturalnumber };
identifier = letter, { letter | digit | "_" };
identifierdeclaration = ":", whitespace, identifier;

(* Structure *)
section = "$", [identifierdeclaration];
measure = "#", [metricalduration], [identifierdeclaration];

(* Relationship *)
relationshipdeclaration = 
	identifier, 
	whitespace, 
	relationshipoperator, 
	whitespace,
	identifier,
	[identifierdeclaration];

relationshipoperator = 
	bidirectionalrelationshipoperator |
	immediateunidirectionalrelationshipoperator |
	delayedunidirectionalrelationshipoperator;

bidirectionalrelationshipoperator = "<>"
immediateunidirectionalrelationshipoperator = "->"
delayedunidirectionalrelationshipoperator = "~>" (* TODO: extend to specify delay by any time interval type *)

(* Metrical Duration *)
metricalduration = int, ",", int;
(* e.g., 2,16 *)

metricaldurationcontainer = 
	metricalduration, 
	[identifier, identifier], 
	[identifierdeclaration];
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
namedpitch = 
	lettername, 
	[([quarterstepmodifier] halfstepindicator)], 
	[eighthstepmodifier];

pitch = float | namedpitch;

