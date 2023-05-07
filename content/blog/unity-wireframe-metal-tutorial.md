---
title: "Tutorial - Unity Wireframe effect for Metal (iOS, Mac)"
date: "2023-05-06"
description: >-
  Want a retro Vectrex like wireframe effect that works on Apple Metal for MacOS
  and iOS development? Well look no further as in this tutorial we will be
  developing an effect that works via a C# script in Unity 2021.3.
cover: >-
  img/wireframe-cover.webp
---

I was recently working on a game prototype for a game and I wanted an effect that looked like the Vectrex or other classic vector games. I first tired using a custom shader but found this would not work on macOS or iOS using Metal, after some researching I came across the method I use in this post to generate the wireframes which is based on a script instead and works with every platform.

First we need to start by opening the Unity Hub and creating a new 3D project with a project name in a directory you use. The version of Unity we are using for this tutorial is 2021.3.23f1 as its the latest LTS at the date of publication.

![Creating a new project in the Unity Hub](/img/wireframe/1.webp)

Create a Cube in the Scene by right clicking on the hierarchy view selecting 3D Object → Cube. Next create a Scripts folder in the Assets view and inside that folder create a script named WireframeRenderer. Then open the script in the editor of your choice (Rider, Visual Studio or Visual Studio Code) and copy the following script below.

```csharp
using System.Collections.Generic;
using UnityEngine;

[RequireComponent( typeof( MeshFilter ) )]
public class WireframeRenderer: MonoBehaviour {

    private const float Distance = 1.0001f;
    private static readonly Color Color = Color.black;
    private List<Vector3> _renderingQueue;

    public Material wireMaterial;

    private void InitializeOnDemand() {
        if (_renderingQueue != null) {
            return;
        }
        var meshFilter = gameObject.GetComponent<MeshFilter>();
        if ( meshFilter == null ) {
            var go = gameObject;
            Debug.LogError( "No mesh detected at" + go.name, go );
            return;
        }
        var mesh = meshFilter.mesh;

        _renderingQueue = new List<Vector3>();
        foreach (var point in mesh.triangles) {
            _renderingQueue.Add( mesh.vertices[point] * Distance );
        }
    }

    public void OnPreRender() {
        GL.wireframe = true;
    }

    public void OnRenderObject() {
        InitializeOnDemand();

        if (wireMaterial != null) {
            wireMaterial.SetPass(0);
        } else {
            var color = Color;
            GL.Color( color );
        }

        GL.MultMatrix( transform.localToWorldMatrix );
        GL.Begin( GL.LINES );

        for ( var i = 0; i < _renderingQueue.Count; i+=3 ) {
            var vertex1 = _renderingQueue[i];
            var vertex2 = _renderingQueue[i+1];
            var vertex3 = _renderingQueue[i+2];
            GL.Vertex3( vertex1.x, vertex1.y, vertex1.z );
            GL.Vertex3( vertex2.x, vertex2.y, vertex2.z );
            GL.Vertex3( vertex2.x, vertex2.y, vertex2.z );
            GL.Vertex3( vertex3.x, vertex3.y, vertex3.z );
            GL.Vertex3( vertex3.x, vertex3.y, vertex3.z );
            GL.Vertex3( vertex1.x, vertex1.y, vertex1.z );
        }
        GL.End();
    }

    public void OnPostRender() {
        GL.wireframe = false;
    }
}
```

This script gets the vertices of the mesh and on render it will draw the GL lines for the object therefore creating a outline of the vertices. This creates a outline but doesn't look that great, but we will fix that after with some post processing.

Next we will need to create a folder named Materials in assets and a material named WireframeMaterial that will have the settings below for the wireframe.

![Creating the Wireframe Material](/img/wireframe/2.webp)

After that create another material called CubeMaterial that will be used to make the cube transparent for a proper wireframe effect, this can be done with the settings below.

![Creating the Cube Material](/img/wireframe/3.webp)

Add the CubeMaterial to the cube to make the cube transparent, after that add the WireframeRenderer script and set the Wire Material to the WireframeMaterial for the outline to have the desired coloured.

Now that is done we need to create the glow so the lines look give a better CRT like effect, this can be done with Unity’s Post Processing plugin. To start open the package manager and search the Unity Registry for Post Processing and install the package.

![Adding Post Processing in Unity Package Manager](/img/wireframe/5.webp)

Once that is done add a post processing layer to the Main Camera and set the layer to a new layer called Post Processing Layer. To have the wireframe look less jaggy set the Anti-aliasing to an enabled state and play around with what works best.

Next create a folder in the assets called Profiles and create a post processing profile named WireframeProfile with the following settings.

![The post processing profile settings suggested](/img/wireframe/6.webp)

Once this is done add this effect to a empty object in the Post Processing Layer with the global effect on and add the Post Processing profile created above. Once this is done you should be able to hit play and get a result like the one below.

![Running the project in the player](/img/wireframe/7.webp)

Hopefully this tutorial was helpful to you and allowed you to create a wireframe while still being able to use Metal and not OpenGL. Check out the tutorial’s source code on GitHub [here](https://github.com/studioripe/wireframe-tutorial), If you have any questions feel free to comment. The code used for the wireframe renderer in this tutorial comes from this asset on the [Unity Store](https://assetstore.unity.com/packages/tools/modeling/mesh-wireframe-renderer-58433) so please show some support to the creator.
