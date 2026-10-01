# 3D asset pipeline

The art was produced by one person with no modelling team. Generated meshes did the bulk of
the work and hand clean-up made them usable.

```
1 Concept            2 Image to 3D          3 Clean-up        4 In game
ChatGPT image    →   Meshy AI / Rodin AI →  Blender       →   Unity import
```

## 1. Concept image

ChatGPT generates a 2D image of how the character or vehicle should look. The mesh generators
in the next step work from a picture, so this image decides most of the outcome.

## 2. Image to mesh

Two generators were used: Meshy AI and Rodin AI. Both turn the concept image into a mesh.
Rodin gave cleaner polygons, so it was the one leaned on. Meshy has a Unity plug-in that
imports directly into the project.

## 3. Clean-up in Blender

Generated meshes are a starting point, not a finished asset. Each one was fine-tuned by hand
in Blender before use.

## 4. Into Unity

The cleaned models are imported into the project as unit models. Content is data-driven, so
a model is assigned through a data asset and swapping a placeholder for a finished model does
not touch code.

## Note

The coding agent was not part of this pipeline. The art tools and the code tools were used
side by side, and the only meeting point was the Unity import.
