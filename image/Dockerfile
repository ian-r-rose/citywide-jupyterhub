FROM jupyter/datascience-notebook

# Having a CLI text editor is nice.
USER root
RUN apt-get update && apt-get install -y vim graphviz
USER $NB_UID

# Install conda dependencies early, as it takes a long time.
RUN conda install -c conda-forge \
  cartopy \
  dask \
  distributed \
  ibis-framework \
  intake \
  intake-parquet \
  matplotlib \
  nodejs \
  numpy \
  scikit-learn \
  scipy \
  xlrd \
  statsmodels \
  geopandas \
  s3fs


# Rebuilding lab also takes a long time.
RUN pip install jupyterlab==1.0.0a5
RUN jupyter labextension install --no-build @jupyterlab/geojson-extension@0.18
RUN jupyter labextension install --no-build @jupyterlab/toc@1.0.0-pre.2
RUN jupyter labextension uninstall --no-build @jupyterlab/hub-extension
RUN jupyter labextension uninstall --no-build jupyterlab_bokeh
RUN jupyter lab build && jupyter lab clean

# These are pretty quick and are python-only, so pip should be okay.
RUN pip install \
  altair \
  descartes \
  folium \
  geoalchemy2 \
  geocoder \
  geopy \
  intake_geopandas>=0.2.2 \
  intake_dcat>=0.2 \
  ipywidgets \
  ipyleaflet \
  mapboxgl \
  openpyxl \
  papermill \
  psycopg2 \
  usaddress \
  vega-datasets

# AWS CLI is kind of a pain, as it has some old, hard dependencies.
run pip install awscli --ignore-installed