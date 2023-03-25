# What? Why? Who? Wazzit?

I'm tried of looking up the same information again and again. I do not like those proprietary solutions, Sam I am. 

I'd rather build a framework that saves us all time than come up with a propratary system that saves me time.

We all have better things to do than put connectors on drawings. 


### ok?

So, at the foundation OpenAVL is a series of text files describing as many AVL devices as possible. Writing this in early 2023 it
looks a lot like eventually AI will read the datasheets mostly well enough for us, but we should save our new overlords some time and
record there efforts into a database. 

### why not a "real" databse?

A flat file human readable storage method means it has the best chance of being future proof and not reliant on some software stack
to be avaible and easy to install. This database will just be some files and as long as we keep copying that floppy it will hopefully
be around for a while. 

### why does THAT matter?

This collection of information will take effort, and we should our best to treat that with respect and make it available for as long
as it is relevant. 



# File Descriptions and Layouts


## equipment.yaml

This is the heart of the project. Although I'm not sure how many times this file will need to be sub divided currently, this is the heart of the project.
Equipment, with manufacturer information, connector information, signal information, and pinouts will all live here. Many of the fields will only be allowed
to be filled by references from the other databases. This is done to try to force the information to be clean. 

What to include and what not to include? Primary goal of this is currently making functional drawings accurate and easy. This includes rack drawings and figuring out power usage. So - with that in mind, currently things that are needed for reference but don't affect functional block diagarms are excluded. This means output lumens of a lighting fixture or projector aren't relevant - however the video resolutions supported by a projector are. As well, DMX footprint size matters, but channel mapping doesnt. 



I'm sure this will get more complicated as we go, but here's the start. 

```
equipment:
  - id: [UUID]
    manufacturer: [Manufacturer]
    name: [Product name, identifier, ect]
    model: [Catalog number, model number, maybe year if you're apple]
    - connectors:
      -connector_number: [INDEX]
        direction: [INPUT/OUTPUT/BIDIRECTIONAL]
        connector_type: [Physical connector populated from 'connector_types.yaml']
        signal_type: [VIDEO, AUDIO, LIGHTING, DATA, CONTROL, MIXED] <--- maybe need more catagories and some "unknowns"
        pinout: [pintout populated from "pinouts.yaml"] <--- may be overlooked, but important to reference 
    - physical:
      width: [mm]
      height: [mm]
      depth: [mm]
      weight: [kg]
      rack_units : [# / NONE]
      votlage: [v]
      wattage: [w]
     notes: [ Used for documenting quirks about using this device ]
      
    ### OPTIONAL ###
    
    - video:
      -resolutions: [ Width x Height x Frame Rate ]
     
     - lighting:
      - dmx_footprint: [ Number of Channels ]
      
     - audio:
      - digital_audio_channels: [# of Dante or Madi or AES67 channels]
      
       
```


