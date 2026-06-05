# Delphi_pipeline_tools

Syntax: ./extract.sh [number_of_events] [config_file] [output_dir_path]

Example: Running ./extract.sh 10 config_z_mm.txt ./output/ will generate 10 events using the builtin Z-> mu mu configuration inside the container. It will extract a simana_data.sdst and a data.root file and place it inside ./output/

To manually enter the container and mess around non-destructively: podman run -it --rm --entrypoint /bin/bash -w /work delphi-complete:v2

Note: This script is meant to be run with this container: https://hub.docker.com/r/alqanb/pythia_delphi_pipeline
