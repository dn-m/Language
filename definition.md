(* General *)
whitespace = " ", "\t" (* others... *);
letter = "a" | ... | "z" | "A" | ... | "Z"; 
digit = "0" | ... | "9";
int = { digit };
float = { digit } , ".", { digit };
identifier = letter, { letter | digit | "_" };
identifierdeclaration = ":", whitespace, identifier;

(* Structure *)
section = "$", [identifierdeclaration];
measure = "#", [metricalduration], [identifierdeclaration];

(* Metrical Duration *)
metricalduration = int, ",", int;

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

