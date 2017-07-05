# gsx_regression

This project holds regression data for the [gsx project](https://bitbucket.org/nsidc/gsx).  When gsx is modified so that the regression data is changed, you will have to update this repository with a new, good version of the output regression data and also update the gsx project to use the correct tag during regression testing.  This tag is located in the gsx project's `gsx/test/regression/config.py` file along with the rest of the regression configuration.


## Overview

This project just holds data, `README.md` and `.bumpversion.cfg`. The minimum usecase to update your data when regressions change is to add your changed regression data to the project, tag it and push it to github.  Then change the regression configuration in `gsx/test/regression/config.py` to use this new tag.

## Quickstart

Use bumpversion to update the repository when you have created new data and then update gsx with the new tag.

1. Clone the repository
2. replace old regression data with new regression data.
3. `cd gsx_regression`
4. `bumpversion major|minor|patch`
5. `git push && git push --tags`
6. **update gsx project with new tag**


## Step-by-step instructions for updating regression data.


1. On your gsx-vm as user vagrant, checkout the master branch of https://github.com/nsidc/gsx_regression into `/vagrant/source/gsx_regression`.

   > `vagrant@gsx-vms:/vagrant/source$ git clone git@github.com:nsidc/gsx_regression.git`

2. Make sure gsx-vm's gsx project is upto date with the latest code you want to create regression data for and checked out into `/vagrant/source/gsx`
   You're about to generate new output values for your regression data, so you want to be certain you have the correct version of gsx checked out.


3. Check to make sure any data that you have generated has the expected differences with the current regression data. ```invoke regression.regression```.  This will take few minutes and the result will be a list regression tests that passed/failed.
If they show all passed, you haven't changed your data, or you don't need to update your regression test.

        PASS: /projects/PMESDR/vagrant/gsx_regression/data/input/csu/CSU_SSMI_FCDR_V01R00_F08_D19870824_S0028_E0210_R00917.nc
		PASS: /projects/PMESDR/vagrant/gsx_regression/data/input/csu/CSU_SSMI_FCDR_V01R00_F08_D19870824_S1222_E1404_R00924.nc
		PASS: /projects/PMESDR/vagrant/gsx_regression/data/input/csu/CSU_SSMI_FCDR_V01R00_F11_D19940824_S1923_E2105_R14133.nc
		PASS: /projects/PMESDR/vagrant/gsx_regression/data/input/csu/CSU_SSMI_FCDR_V01R00_F13_D19960322_S0056_E0238_R05133.nc
		PASS: /projects/PMESDR/vagrant/gsx_regression/data/input/amsre/AMSR_E_L2A_BrightnessTemperatures_V12_200206012358_A.hdf
		PASS: /projects/PMESDR/vagrant/gsx_regression/data/input/amsre/AMSR_E_L2A_BrightnessTemperatures_V12_200308080121_D.hdf
		PASS: /projects/PMESDR/vagrant/gsx_regression/data/input/amsre/AMSR_E_L2A_BrightnessTemperatures_V12_200604090129_A.hdf
		PASS: /projects/PMESDR/vagrant/gsx_regression/data/input/amsre/AMSR_E_L2A_BrightnessTemperatures_V12_201109092327_D.hdf
		PASS: /projects/PMESDR/vagrant/gsx_regression/data/input/rss/RSS_SSMI_FCDR_V07R00_F08_D19870824_S0419_E0514_R00919.nc
		PASS: /projects/PMESDR/vagrant/gsx_regression/data/input/rss/RSS_SSMI_FCDR_V07R00_F08_D19870824_S1334_E1526_R00925.nc
		PASS: /projects/PMESDR/vagrant/gsx_regression/data/input/rss/RSS_SSMI_FCDR_V07R00_F11_D19940824_S2034_E2226_R14134.nc
		PASS: /projects/PMESDR/vagrant/gsx_regression/data/input/rss/RSS_SSMI_FCDR_V07R00_F13_D19960322_S0058_E0218_R05133.nc
		PASS: /projects/PMESDR/vagrant/gsx_regression/data/input/rss/RSS_SSMI_FCDR_V07R00_F13_D20030808_S0119_E0311_R43204.nc
        PASS: /projects/PMESDR/vagrant/gsx_regression/data/input/rss/RSS_SSMI_FCDR_V07R00_F13_D20030831_S2304_E0056_R43542.nc

4. Generate new regresssion data   ```invoke regression.regenerate_regression_data```.  This generates new output regression data using the current gsx.  The output is a list of tuples of the input file and output file.


		('/projects/PMESDR/vagrant/gsx_regression/data/input', 'regenerated-data')
		('/projects/PMESDR/vagrant/gsx_regression/data/input/csu/CSU_SSMI_FCDR_V01R00_F08_D19870824_S0028_E0210_R00917.nc', 'regenerated-data/csu/GSX_CSU_SSMI_FCDR_V01R00_F08_D19870824_S0028_E0210_R00917.nc')
		('/projects/PMESDR/vagrant/gsx_regression/data/input/csu/CSU_SSMI_FCDR_V01R00_F08_D19870824_S1222_E1404_R00924.nc', 'regenerated-data/csu/GSX_CSU_SSMI_FCDR_V01R00_F08_D19870824_S1222_E1404_R00924.nc')
		('/projects/PMESDR/vagrant/gsx_regression/data/input/csu/CSU_SSMI_FCDR_V01R00_F11_D19940824_S1923_E2105_R14133.nc', 'regenerated-data/csu/GSX_CSU_SSMI_FCDR_V01R00_F11_D19940824_S1923_E2105_R14133.nc')
		('/projects/PMESDR/vagrant/gsx_regression/data/input/csu/CSU_SSMI_FCDR_V01R00_F13_D19960322_S0056_E0238_R05133.nc', 'regenerated-data/csu/GSX_CSU_SSMI_FCDR_V01R00_F13_D19960322_S0056_E0238_R05133.nc')
		('/projects/PMESDR/vagrant/gsx_regression/data/input/amsre/AMSR_E_L2A_BrightnessTemperatures_V12_200206012358_A.hdf', 'regenerated-data/amsre/GSX_AMSR_E_L2A_BrightnessTemperatures_V12_200206012358_A.nc')
		('/projects/PMESDR/vagrant/gsx_regression/data/input/amsre/AMSR_E_L2A_BrightnessTemperatures_V12_200308080121_D.hdf', 'regenerated-data/amsre/GSX_AMSR_E_L2A_BrightnessTemperatures_V12_200308080121_D.nc')
		('/projects/PMESDR/vagrant/gsx_regression/data/input/amsre/AMSR_E_L2A_BrightnessTemperatures_V12_200604090129_A.hdf', 'regenerated-data/amsre/GSX_AMSR_E_L2A_BrightnessTemperatures_V12_200604090129_A.nc')
		('/projects/PMESDR/vagrant/gsx_regression/data/input/amsre/AMSR_E_L2A_BrightnessTemperatures_V12_201109092327_D.hdf', 'regenerated-data/amsre/GSX_AMSR_E_L2A_BrightnessTemperatures_V12_201109092327_D.nc')
		('/projects/PMESDR/vagrant/gsx_regression/data/input/rss/RSS_SSMI_FCDR_V07R00_F08_D19870824_S0419_E0514_R00919.nc', 'regenerated-data/rss/GSX_RSS_SSMI_FCDR_V07R00_F08_D19870824_S0419_E0514_R00919.nc')
		('/projects/PMESDR/vagrant/gsx_regression/data/input/rss/RSS_SSMI_FCDR_V07R00_F08_D19870824_S1334_E1526_R00925.nc', 'regenerated-data/rss/GSX_RSS_SSMI_FCDR_V07R00_F08_D19870824_S1334_E1526_R00925.nc')
		('/projects/PMESDR/vagrant/gsx_regression/data/input/rss/RSS_SSMI_FCDR_V07R00_F11_D19940824_S2034_E2226_R14134.nc', 'regenerated-data/rss/GSX_RSS_SSMI_FCDR_V07R00_F11_D19940824_S2034_E2226_R14134.nc')
		('/projects/PMESDR/vagrant/gsx_regression/data/input/rss/RSS_SSMI_FCDR_V07R00_F13_D19960322_S0058_E0218_R05133.nc', 'regenerated-data/rss/GSX_RSS_SSMI_FCDR_V07R00_F13_D19960322_S0058_E0218_R05133.nc')
		('/projects/PMESDR/vagrant/gsx_regression/data/input/rss/RSS_SSMI_FCDR_V07R00_F13_D20030808_S0119_E0311_R43204.nc', 'regenerated-data/rss/GSX_RSS_SSMI_FCDR_V07R00_F13_D20030808_S0119_E0311_R43204.nc')
		('/projects/PMESDR/vagrant/gsx_regression/data/input/rss/RSS_SSMI_FCDR_V07R00_F13_D20030831_S2304_E0056_R43542.nc', 'regenerated-data/rss/GSX_RSS_SSMI_FCDR_V07R00_F13_D20030831_S2304_E0056_R43542.nc')

5. Test it: ```$ invoke regression.do_regression --source-dir="/projects/PMESDR/vagrant/gsx_regression/data/input/" --expected-dir="./regenerated-data"```

	This tests input data vs the data you just generated, this really, **really** should match and show all passes.

		vagrant@vmsnowyverglas /vagrant/source/tasks (master *=)
		$ invoke regression.do_regression --source-dir="/projects/PMESDR/vagrant/gsx_regression/data/input/" --expected-dir="./regenerated-data"
		/vagrant/source/gsx/strategies/rss.py:299: RuntimeWarning: invalid value encountered in less
		  a_prime[a_prime < 0] = 360.0 + a_prime[a_prime < 0]
		PASS: /projects/PMESDR/vagrant/gsx_regression/data/input/csu/CSU_SSMI_FCDR_V01R00_F08_D19870824_S0028_E0210_R00917.nc
		PASS: /projects/PMESDR/vagrant/gsx_regression/data/input/csu/CSU_SSMI_FCDR_V01R00_F08_D19870824_S1222_E1404_R00924.nc
		PASS: /projects/PMESDR/vagrant/gsx_regression/data/input/csu/CSU_SSMI_FCDR_V01R00_F11_D19940824_S1923_E2105_R14133.nc
		PASS: /projects/PMESDR/vagrant/gsx_regression/data/input/csu/CSU_SSMI_FCDR_V01R00_F13_D19960322_S0056_E0238_R05133.nc
		PASS: /projects/PMESDR/vagrant/gsx_regression/data/input/amsre/AMSR_E_L2A_BrightnessTemperatures_V12_200206012358_A.hdf
		PASS: /projects/PMESDR/vagrant/gsx_regression/data/input/amsre/AMSR_E_L2A_BrightnessTemperatures_V12_200308080121_D.hdf
		PASS: /projects/PMESDR/vagrant/gsx_regression/data/input/amsre/AMSR_E_L2A_BrightnessTemperatures_V12_200604090129_A.hdf
		PASS: /projects/PMESDR/vagrant/gsx_regression/data/input/amsre/AMSR_E_L2A_BrightnessTemperatures_V12_201109092327_D.hdf
		PASS: /projects/PMESDR/vagrant/gsx_regression/data/input/rss/RSS_SSMI_FCDR_V07R00_F08_D19870824_S0419_E0514_R00919.nc
		PASS: /projects/PMESDR/vagrant/gsx_regression/data/input/rss/RSS_SSMI_FCDR_V07R00_F08_D19870824_S1334_E1526_R00925.nc
		PASS: /projects/PMESDR/vagrant/gsx_regression/data/input/rss/RSS_SSMI_FCDR_V07R00_F11_D19940824_S2034_E2226_R14134.nc
		PASS: /projects/PMESDR/vagrant/gsx_regression/data/input/rss/RSS_SSMI_FCDR_V07R00_F13_D19960322_S0058_E0218_R05133.nc
		PASS: /projects/PMESDR/vagrant/gsx_regression/data/input/rss/RSS_SSMI_FCDR_V07R00_F13_D20030808_S0119_E0311_R43204.nc
		PASS: /projects/PMESDR/vagrant/gsx_regression/data/input/rss/RSS_SSMI_FCDR_V07R00_F13_D20030831_S2304_E0056_R43542.nc


6. Move the data into the local `/vagrant/source/gsx_regression` project using
   ```invoke regression.relocate_regenerated --old-root=/vagrant/source/gsx_regression/data/expected/```
    This doesn't have any output, but all of the files generated in `regenerated-data` into the clone of `gsx_regression` you checked out in step 1.

7. Look at the local gsx_regression clone checked out in `/vagrant/source/gsx_regression`.
   You will see that all of the netcdf files have changed.

		   $ git status
		On branch master
		Your branch is up-to-date with 'origin/master'.
		Changes not staged for commit:
		  (use "git add <file>..." to update what will be committed)
		  (use "git checkout -- <file>..." to discard changes in working directory)

				modified:   data/expected/amsre/GSX_AMSR_E_L2A_BrightnessTemperatures_V12_200206012358_A.nc
				modified:   data/expected/amsre/GSX_AMSR_E_L2A_BrightnessTemperatures_V12_200308080121_D.nc
				modified:   data/expected/amsre/GSX_AMSR_E_L2A_BrightnessTemperatures_V12_200604090129_A.nc
				modified:   data/expected/amsre/GSX_AMSR_E_L2A_BrightnessTemperatures_V12_201109092327_D.nc
				modified:   data/expected/csu/GSX_CSU_SSMI_FCDR_V01R00_F08_D19870824_S0028_E0210_R00917.nc
				modified:   data/expected/csu/GSX_CSU_SSMI_FCDR_V01R00_F08_D19870824_S1222_E1404_R00924.nc
				modified:   data/expected/csu/GSX_CSU_SSMI_FCDR_V01R00_F11_D19940824_S1923_E2105_R14133.nc
				modified:   data/expected/csu/GSX_CSU_SSMI_FCDR_V01R00_F13_D19960322_S0056_E0238_R05133.nc
				modified:   data/expected/rss/GSX_RSS_SSMI_FCDR_V07R00_F08_D19870824_S0419_E0514_R00919.nc
				modified:   data/expected/rss/GSX_RSS_SSMI_FCDR_V07R00_F08_D19870824_S1334_E1526_R00925.nc
				modified:   data/expected/rss/GSX_RSS_SSMI_FCDR_V07R00_F11_D19940824_S2034_E2226_R14134.nc
				modified:   data/expected/rss/GSX_RSS_SSMI_FCDR_V07R00_F13_D19960322_S0058_E0218_R05133.nc
				modified:   data/expected/rss/GSX_RSS_SSMI_FCDR_V07R00_F13_D20030808_S0119_E0311_R43204.nc
				modified:   data/expected/rss/GSX_RSS_SSMI_FCDR_V07R00_F13_D20030831_S2304_E0056_R43542.nc

	This is because the new netcdf files have a `gsx_date_created` tag.  I would discard changes to any files that show modified, but that weren't actually changed.  Say you were working on CSU changes only, you know rss and amsre diffs are just the date tag. so discard all of those changes.

		$ git status
		On branch master
		Your branch is up-to-date with 'origin/master'.
		Changes not staged for commit:
		  (use "git add <file>..." to update what will be committed)
		  (use "git checkout -- <file>..." to discard changes in working directory)

				modified:   data/expected/csu/GSX_CSU_SSMI_FCDR_V01R00_F08_D19870824_S0028_E0210_R00917.nc
				modified:   data/expected/csu/GSX_CSU_SSMI_FCDR_V01R00_F08_D19870824_S1222_E1404_R00924.nc
				modified:   data/expected/csu/GSX_CSU_SSMI_FCDR_V01R00_F11_D19940824_S1923_E2105_R14133.nc
				modified:   data/expected/csu/GSX_CSU_SSMI_FCDR_V01R00_F13_D19960322_S0056_E0238_R05133.nc

		no changes added to commit (use "git add" and/or "git commit -a")


8. Checkin the new files to the project.
	`$ git add -u .`
    `$ git commit -m "updated regression data for described changes"`


9. Tag the project.
    `$ git tag {tagvalue} master`


10. push it all.
	`$ git push origin master`
	`$ git push origin --tags`

11.  Change the gsx config to use the new data.
     Set `/vagrant/source/gsx/test/regression/config.py` tag value to the tag you just made.
     `tag = "{tagvalue}"`
     Commit and push that to the gsx repository.
