🧬 Agarose Gel Annotation Guidelines & Taxonomy StandardsThis document outlines the standard operating procedure (SOP) for annotating agarose gel electrophoresis images for computer vision instance segmentation and object detection models.

🏷️ Class Definitions & Geometry RulesClass IDClass NameGeometry TypeAnnotation Criteria & Boundary Rules0WellPolygon / BoxOutline the rectangular sample loading wells located at the top of the gel matrix. Include the visible outline of the gel pocket.

1ArtifactPolygonOutline non-biological visual noise, dust particles, air bubbles, gel tears, or camera reflection glares that do not represent DNA features.

2DNA_LadderBounding BoxEnclose the entire vertical reference ladder lane from the top band down to the lowest visible benchmark band.

3Gel_LaneBounding BoxEnclose the full length of an individual sample lane, starting below the loading well down to the gel dye front.
4DNA_BandPolygonDraw a tight contour mask around distinct, illuminated target PCR product bands. The boundary must closely hug the signal edge without capturing background noise.5Negative controlBounding BoxEnclose the entire lane designated for the negative control reaction (e.g., master mix without template DNA).6Control/No_AmpBounding BoxOutline specific reaction wells or lane regions where no amplification was observed (absence of target PCR band).7Ladder_BandPolygonDraw tight polygon contours around individual benchmark bands within the molecular ladder (DNA_Ladder). Assign the size_bp attribute where applicable (e.g., 500bp, 1000bp).8DNA_SmearPolygon / BoxEnclose continuous, diffuse vertical streaks indicating degraded DNA, over-loaded samples, or non-specific amplification across a lane segment.


📐 General Annotation Quality RulesPolygon Tightness: For DNA_Band and Ladder_Band, avoid loose bounding boxes. Polygon vertices must tightly map the fluorescent perimeter of the DNA signal.Overlapping Features: Smaller sub-features (e.g., Ladder_Band) live inside macro-structures (e.g., DNA_Ladder). Both should be annotated independently to support multi-scale evaluation.Faint Bands: Any signal visible to the human eye above background noise should be annotated as a band, with its metadata attribute set to Intensity: Low.Artifact Isolation: If an artifact directly touches a DNA_Band, segment the band clean up to the artifact border and annotate the artifact separately under Class 1.
