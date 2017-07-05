# gsx_regression

This project holds regression data for the [gsx project](https://bitbucket.org/nsidc/gsx).  When gsx is modified so that the regression data is changed, you will have to update this repository with a new good version of the regression data and then update the gsx project to use the correct tag.  There are easy steps to do this documented in the gsx README.md file.

## Quickstart

This project just holds data, this README and a .bumpversion.cfg.  Use
bumpversion to update the repository when you have created new data and then
update gsx with the new tag.

1. Clone the repository
2. `cd gsx_regression`
3. `bumpversion major|minor|patch`
4. `git push && git push --tags`
5. **update gsx with new tag**


## Steps for updating regression data.

1. On your gsx-vm as user vagrant.  checkout the master branch of this project located in the `/projects/PMESDR/vagrant/gsx_regression` directory into `~/gsx_regression`.

2. Make sure gsx-vm's gsx project is upto date with the latest code you want to create regression data for and checked out into `~/gsx`

3. Check to make sure any data that you have generated has the expected differences with the current regression data. ```invoke regression.regression```

4. regenerate regresssion data   ```invoke regression.regenerate_regression_data```

5. Test it:     ```invoke regression.do_regression:source_dir=~/gsx_regression/data/input/,expected_dir=~/gsx/regenerated-data```

6. Move the data into the local `~/gsx_regression` project     ```invoke regression.relocate_regenerated:old_root=~/gsx_regression/data/expected/```

7. You will probably have to prune files that didn't change, but only their times.  aka, AMSRE files if only SSMI changes were introduced.

8. Checkin the new files.

9. Tag the project.

10. push it all.
