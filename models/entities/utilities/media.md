# MACH Alliance • Open Data Model

# Utility Object: `Media`

## Table of contents
- [Purpose](#purpose)
- [Object: Media](#object-media)
- [Sample Objects: Image](#sample-objects-media-type-image)
- [Sample Objects: Video](#sample-objects-media-type-video)
- [Implementation Guidelines](#implementation-guidelines)
- [Media Type Examples](#media-type-examples)
- [Related Utility Objects](#related-utility-objects)

---

## Purpose

A standardized utility object for representing media assets across all entities in the MACH Alliance Common Data Model. This ensures consistent handling of images, videos, documents, and other digital assets across commerce engines, content management systems, digital asset management systems, and product information management systems.

The Media utility object provides:
- Standardized media asset representation
- Consistent URL and metadata handling
- Support for multiple media types
- Responsive image handling
- Asset optimization and delivery

---

## Object: Media

| Field               | Description                                                                                         | Practice     |
|--------------------|-----------------------------------------------------------------------------------------------------|--------------|
| `id`               | Unique identifier for the media asset                                                               | SHOULD       |
| `type`             | Type of media asset (`image`, `video`, `document`, `audio`, `3d`)                                   | SHOULD       |
| `status`           | Lifecycle status of the asset (`published`, `active`, `archived`)                                   | SHOULD        |
| `referenceIds`     | Platform-specific references (e.g., PIM ID, DAM asset ID, CMS entry ID)                             | COULD        |
| `createdAt`        | ISO timestamp of asset creation                                                                     | SHOULD       |
| `updatedAt`        | ISO timestamp of last modification                                                                  | SHOULD       |
| `title`            | Human-readable name or headline for the asset                                                       | SHOULD       |
| `description`      | Descriptive text about the asset’s content and purpose                                              | RECOMMENDED  |
| `tags`             | Array of taxonomy keywords or labels                                                                | COULD        |
| `file`             | Core file object with technical details like `url`, `format`, `sizeBytes`, and dimensions/duration  | SHOULD       |
| `thumbnail`        | Optional reduced-size visual or preview version                                                     | RECOMMENDED  |
| `accessibility`    | Object with `altText`, `longDescription`, `decorative`, and optional contrast data                  | SHOULD       |
| `traits.rights`    | Copyright, usage terms, creator attribution, and expiration                                         | RECOMMENDED  |
| `traits.associations` | Product and category references, campaign IDs, taxonomy links                                   | COULD        |


---

## Sample Object: Image

This example illustrates a high-resolution image asset used in a composable setup, complete with metadata, responsive formats, focal point, accessibility features, and platform-specific references across PIM, DAM, and CMS.



```jsonc

{
  "id": "img-001987",
  "type": "image",
  "status": "published",
  "referenceIds": {
    "pim": "pim-99871",
    "dam": "asset-1842356",
    "cms": "entry-9d22bfa",
  },
  "createdAt": "2025-07-08T13:00:00Z",
  "updatedAt": "2025-07-09T09:15:00Z",
  "title": "Yellow MACH Alliance T-Shirt Front View",
  "description": "Studio image of a yellow MACH Alliance t-shirt with a small embroidered logo on the left chest, photographed on a clean white background.",
  "tags": ["mach-alliance", "tshirt", "yellow", "apparel", "branded", "merchandise"],
  "file": {
    "url": "https://cdn.example.com/assets/img-001987.webp",
    "format": "webp",
    "sizeBytes": 1032840,
    "width": 2400,
    "height": 1600,
  },
  "thumbnail": {
    "url": "https://cdn.example.com/assets/img-001987-thumb.webp",
    "format": "webp",
    "sizeBytes": 85240,
    "width": 480,
    "height": 320
  },
  "focalPoint": {
    "x": 0.32,
    "y": 0.35,
    "description": "Center of the embroidered MACH Alliance logo on the left chest"
  },
  "accessibility": {
    "altText": "Yellow MACH Alliance t-shirt with a small embroidered logo on the chest.",
    "longDescription": "This is a high-resolution studio photograph of a bright yellow t-shirt, laid flat against a white background. The shirt features a subtle MACH Alliance embroidered logo in black, located on the left chest area. The fabric texture and stitching are clearly visible, and the lighting is balanced to emphasize detail without shadows.",
    "decorative": false,
    "contrastCheck": {
      "background": "#FFFFFF",
      "foreground": "#FFD700",
      "contrastRatio": 1.1,
      "passesAA": false,
      "passesAAA": false
    }
  },
  "traits": {
    "rights": {
      "copyright": "© 2025 MACH Alliance",
      "usageTerms": "Unlimited commercial and editorial use. No expiration.",
      "creator": "Adam Peter Nielsen",
      "expires": null
    },
    "associations": {
      "productIds": ["MACH-TSHIRT-YELLOW-2025"],
      "categories": ["merch", "apparel", "mach-alliance"]
    }
  }
}


```





## Sample Object: Video

This sample shows how a video asset is structured for multi-platform delivery, including playback traits, thumbnail support, usage rights, and direct links to DAM, YouTube, and headless CMS instances.


```jsonc

{
  "id": "vid-000561",
  "type": "video",
  "status": "active",
  "referenceIds": {
    "pim": "pim-vid-23391",
    "dam": "asset-vid-8090",
    "youtube": "dQw4w9WgXcQ",
    "contentful": "entry-bv9d85dd"
  },
  "createdAt": "2025-07-01T09:20:00Z",
  "updatedAt": "2025-07-09T08:35:00Z",
  "title": "How to Assemble the Yellow MACH Alliance statuette",
  "description": "Step-by-step tutorial video showing how to unpack and assemble the MACH Alliance statuette.",
  "tags": ["assembly", "mach-alliance", "tutorial", "unboxing", "swag", "video"],
  "file": {
    "url": "https://cdn.example.com/assets/vid-000561.mp4",
    "format": "mp4",
    "sizeBytes": 104328304,
    "durationSeconds": 148,
    "resolution": "1920x1080",
    "frameRate": 30,
    "bitrateKbps": 4500,
    "audioChannels": "stereo"
  },
  "thumbnail": {
    "url": "https://cdn.example.com/assets/thumbnails/vid-000561-thumb.webp",
    "format": "webp",
    "sizeBytes": 78412,
    "width": 640,
    "height": 360
  },
  "traits": {
    "rights": {
      "copyright": "secret",
      "usageTerms": "Unlimited commercial use across owned and third-party platforms. Attribution not required.",
      "expires": null
    },
    "associations": {
      "productIds": ["MACH-TSHIRT-YELLOW-2025"],
      "categories": ["tutorials", "support", "video-assets"]
    },
    "playback": {
      "autoplay": false,
      "defaultPlaybackSpeed": 1.0,
      "availableSpeeds": [0.5, 1.0, 1.5, 2.0],
      "captionsAvailable": true,
      "transcriptAvailable": true,
      "platforms": {
        "youtube": "https://www.youtube.com/watch?v=dQw4w9WgXcQ"
      }
    }
  }
}




```

---

## Implementation Guidelines

### Media Types
- **image**: Photos, graphics, icons
- **video**: Video files, animations
- **document**: PDFs, documents, specifications
- **audio**: Sound files, podcasts
- **3d**: 3D models, AR assets

### File Formats
- **Images**: jpg, jpeg, png, gif, webp, svg
- **Videos**: mp4, webm, avi, mov
- **Documents**: pdf, doc, docx, txt
- **Audio**: mp3, wav, aac, ogg

### URL Guidelines
- Use HTTPS URLs for security
- Consider CDN URLs for performance
- Support multiple image sizes/resolutions
- Include versioning for cache busting

### Accessibility
- Always include meaningful `alt` text
- Use descriptive `label` fields
- Consider screen reader compatibility
- Provide alternative formats when needed

### Best Practices
- Always include `url`, `alt`, and `type` fields
- Use consistent naming conventions for labels
- Optimize images for web delivery
- Consider lazy loading for performance
- Implement proper error handling for broken URLs

### Responsive Images
- Provide multiple sizes for different devices
- Use appropriate formats (WebP for modern browsers)
- Consider aspect ratios for different layouts
- Implement proper fallbacks

---

## Media Type Examples

| Type | Common Formats | Use Cases |
|------|----------------|-----------|
| image | jpg, png, webp, svg | Product photos, banners, icons |
| video | mp4, webm | Product demos, tutorials, ads |
| document | pdf, doc, txt | Size charts, manuals, specs |
| audio | mp3, wav | Product sounds, podcasts |
| 3d | glb, gltf | AR/VR experiences, 3D models |

---

## Related Utility Objects

- **Product**: Product information with media assets
- **Category**: Category images and banners
- **Campaign**: Campaign creative assets
- **Money**: Monetary values for media licensing

---

> This MACH Alliance Canonical Data Model is intentionally __vendor-neutral__ and serves as a foundation for interoperability across composable architectures. It is __continually evolving__ through community contributions, which are reviewed and approved collaboratively.
>
> All contributions are made under the __Creative Commons Attribution 4.0 International License (CC BY 4.0)__. By submitting a contribution, you agree to license your content under <a href="https://creativecommons.org/licenses/by/4.0/deed.en">CC BY 4.0</a>, allowing others to share and adapt the material with proper attribution. 
