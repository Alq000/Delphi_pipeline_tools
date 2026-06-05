# Delphi_pipeline_tools

Note: This script is meant to be run with this container: https://hub.docker.com/r/alqanb/pythia_delphi_pipeline

**Syntax:**
```./extract.sh [number_of_events] [config_file] [output_dir_path]```

**Example:** 
Running ```./extract.sh 10 sample_config_z_mm.txt ./output/``` will generate 10 events. It will extract a simana_data.sdst and a data.root file and place it inside ./output/

**Output:**
data.root
simana_data.sdst

Both these files have the same data but in different formats for convenience. 

To manually enter the container and mess around non-destructively: 
```podman run -it --rm --entrypoint /bin/bash -w /work delphi-complete:v2```

Inside the container are a bunch of preset configs for different collisions, but for quick testing, the sample config file (for Z -> mu mu collisions) is quite useful.


**How to deal with data.root:**
If you aren't familier with the root file format, it's actually not too bad. These are basic commands to get you started:

To open data.root
```root data.root```

This command essentially horizontally concatenates t and tgen, allowing you to compare properties of the same events together. Where t is the reconstructed event data and tgen is the generated event data.

```t->AddFriend(tgen, "tg")```

This draws the transverse momentum distribution of reconstructed particles of events containing exactly 2 particles
```t->Draw("sqrt(px**2+py**2)", "nParticle == 2);```

This draws a histogram of the transverse momentum residuals between reconstructed and generated particle values for events containing exactly 2 particles
```t->Draw("sqrt(px**2+py**2) - sqrt(tg.px**2+tg.py**2)", "nParticle == 2");```

This command draws a histogram of the invariant mass of events containing exactly 2 particles
```t->Draw("sqrt( pow(sqrt(px[0]**2+py[0]**2+pz[0]**2+mass[0]**2) + sqrt(px[1]**2+py[1]**2+pz[1]**2+mass[1]**2), 2) - (pow(px[0]+px[1],2) + pow(py[0]+py[1],2) + pow(pz[0]+pz[1],2)) )", "nParticle == 2")```

**Official data:**
CERN has released official DELPHI simulation data, which can be very useful if you intend to compare data. For Z -> mu mu collisions: https://opendata.cern.ch/record/91079
