(* General *)
whitespace = " ", "\t" (* others... *);
letter = "a" | ... | "z" | "A" | ... | "Z"; 
digit = "0" | nonzerodigit;
nonzerodigit = "1" | "2" | "3" | "4" | "5" | "6" | "7" | "8" | "9"; 
zero = "0";
naturalnumber = nonzerodigit, { digit }
int = ["-"], naturalnumber ;
float = { naturalnumber } , ".", { naturalnumber };
identifier = letter, { letter | digit | "_" };
identifierdeclaration = ":", whitespace, identifier;

(* Structure *)
section = "$", [identifierdeclaration];
measure = "#", [metricalduration], [identifierdeclaration];

(* Metrical Duration *)
metricalduration = int, ",", int;
metricaldurationcontainer = 
	metricalduration, 
	[identifier, identifier], 
	[identifierdeclaration]
;

(* Pitch *)
lettername = "a" | ... | "g" | "A" | ... | "Z" 
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
	[eighthstepmodifier]
;

pitch = float | namedpitch;

