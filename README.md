# CREG12.L75-REF08 <br>
This reprository hold #1 the NEMO code source as associated input files as well (hereafter namelists) and #2 the list of other input files to describe the grid, the bathymetry and the surface forcing used to perform the numerical experiment named CREG12.L75-REF08.<br>

## OVERVIEW
CREG12.L75-REF08 is an ocean/sea-ice numerical experiment that relies on the NEMO numerical plateform [NEMO](https://www.nemo-ocean.eu). It aims at simulating the ocean/sea-ice dynamics over the north Atlantic ocean (starting from ~25°N), the Greenland-Iceland-Norway seas and the whole Arctic basin with a limit along the Bering strait.<br>
* The horizontal grid is a 1/12 degree i.e. from ~8km up to ~4km in most of the Arctic basin.
* A 75 vertical levels from 1m close to the surface up to 200m below 4000m.
* The model time step ∆t=360s for most of the experiment while to get rid of few numerical instabilities, it has been reduced to 288s over some periods.
* The period simulated spans the range 1979-2015.

### SOURCE CODE : 
   * The ocean/sea ice model: <br>
	** The initial code source relies on the official NEMO release 3.6. Information can be found there https://forge.ipsl.jussieu.fr/nemo/wiki/Users#. The whole official code [NEMO](./NEMOGCM/NEMO) is available as the specific code changes as well associated to this experiement in the [MY_SRC](./NEMOGCM/CONFIG/CREG12.L75-REF08/MY_SRC). The [ARCH](./NEMOGCM/ARCH) give a list all computers architecture on wich NEMO has been compiled as templates.
   * The XIOS libray to perform outputs:<br>
	** Outputs have been realised in using the XIOS library; the revision 952 has been downloaded and compiled. More information can be found there [XIOS](https://forge.ipsl.jussieu.fr/nemo/chrome/site/doc/NEMO/guide/html/install.html#extract-and-install-xios).

### INPUT FILES :
1 - Time invariant input files:
   * Bathymetry: <br>
	** Description: ocean depth in meters (zeo aver land grid points). This file has been extracted from an existing global ORCA12 configuration file.<br>
	** File name: ```bathymetry_CREG12_V3.3_CT20180612Larger_ct20190102.nc```<br>
   * Coordinates: <br>
	** Description: horizontal grid scale factors as the geographical location of each Arakaw-C grid type point. This file has been extracted from an existing global ORCA12 configuration file.  <br>
	** File name: ```coordinates_CREG12_lbclnk_noz_vh20160930.nc```<br>
   * Ocean initialisation: <br>
	** Description: World Ocean Atlas 2009 at 1°x1° climatology <br>
	** File name:```woa09_temperature_monthly_1deg_t_an_CMA_drowned_Ex_L75.nc, woa09_salinity_monthly_1deg_s_an_CMA_drowned_Ex_L75.nc``` <br>
   * Ice initialisation:<br>
	** Description: January climatology computed over the period 1998-2007 from a global ocean numerical experiement called ORCA12.L46-MAL95. <br>
	** File name:```CREG12.L75_ORCA12.L46-MAL95_y1998-2007m01_icemod.nc```<br>
   * Tidal mixing parametrization: <br>
	** Description: A new comprehensive parameterization of mixing by breaking internal tides and lee waves (de Lavergne et al., 2019) <br>
	** File name:```mixing_power_bot.nc, mixing_power_pyc.nc, mixing_power_cri.nc, decay_scale_bot.nc, decay_scale_cri.nc``<br>
   * Distance to the coast:<br>
	** Description: gives the distance to the coast of each ocean grid points. It is used to switch off the SSS restoring in a 400km wide range from the coast.<br>
	** File name: ```dist_coast_CREG12_vh_ct20190401.nc```<br>

2 - Time varying input files:
   * Surface forcing:<br>
	** Description: The atmospheric forcing data set so called [DFS5.2](https://ige-meom-opendap.univ-grenoble-alpes.fr/thredds/catalog/meomopendap/extract/ORCA025.L75/ORCA025.L75-GJM189/FORCING_FILES/catalog.html), with ```CORE bulk formulae``` (from NCAR) and relative winds (ocean surface velocity components taken into account for the wind stress<br>
	** File name: ```drowned_u10_DFS5.2_<var>.nc``` <var> stands for either u10,v10,radsw,radlw,precip,snow,t2,q2.<br>
	** Frequency: 3 hours for the wind components u10,v10 and both air humidity and temperature q2 and t2 respectively; 24 hours for radiative (radlw, radsw) and both precipitation and snow fluxes.<br>
   * Rivers and Greenland melting fluxes:<br>
	** Description: A blend of data from Dai & Trenberth for rivers volume fluxes and Bamber for fresh water resulting from Greenland melting<br>
	** File name: ```CREG12_runoff_monthly_combined_Dai_Trenberth_Bamber.nc``<br>
	** Frequency: monthl<br>
   * Open boundaries:<br>
	** Description: 2 open boundaries conditions limit the regional domain, data are used there to force the model and are extracted from a previous global numercial simulation called EORCA12.L75-MJMgd16<br>
	** File name: ```EORCA12.L75-MJMgd16-CREG12.L75-BDY_south_<var>.nc``` and ```EORCA12.L75-MJMgd16-CREG12.L75-BDY_northLarger_<var>.nc```. <var> stands vor SSH, U, V, T, S and ice for the Bering open boundar<br>
	** Frequency: monthly <br>
   * Chlorophyll climatology:<br>
	** Description: Seawiffs satellite data climatology over the period 1999-2900<br>
	** File name: ```chlaseawifs_c1m-99-05_smooth_CREG_R12_vh20161005.nc``<br>
	** Frequency: monthly<br>
   * World Ocean Atlas 2009 surface salinity:<br>
	** Description: Sea surface salinity restoring with a piston velocity of 167 mm/day ( 60 days/10 meters<br>
	** File name: ```woa09_sst01-12_monthly_1deg_t_an_CMA_drowned_Ex_L75.nc```<br>
	** Frequency: monthly<br>
   * World Ocean Atlas 2009 surface temperature:<br>
	** Description: to avoid SSS restoring where the SST climatology temperature is at the freezing point, i.e. in presence of sea-ice<br>
	** File name: ```woa09_sss01-12_monthly_1deg_s_an_CMA_drowned_Ex_L75.nc```<br>
	** Frequency: monthly<br>
