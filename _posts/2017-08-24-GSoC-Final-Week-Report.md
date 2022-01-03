---
category: post
---
#### Introduction to Koko
Koko is a simple image gallery application that is designed to view, edit and share the images.

### GSoC Project Title: Migrating to Kirigami (Koko)
**GSoC 2017 report for my project is at [KDE community wiki](https://community.kde.org/GSoC/2017/StatusReports/atulsharma)**
#### Brief about the project
* Mostly the work is to port the QtQuick Controls elements of Koko image gallery application to Kirigami or QtQuick Controls 2.
* While actually implementing the project, editings were also made to the C++ models used in the application in order to have a better implementation of the Qt's Model-View framework.
* Kirigami elements are introduced into the application such as OverlayDrawers, Kirigami's Page/ScrollablePage
* The Qt Quick Controls elements are replaced by their corresponding Qt Quick Controls 2 elements
* Sharing, Deleting actions have been introduced
* Changing the brightness is possible now
* Touch and hold gestures are available for the mobile UI

#### Changes related to the Model-View framework

* The ImageFolderModel used for representing the images in "By Folder" filter now inherits KDirModel instead of fetching results from the database, while the rest of model fetches the data from the database created by the "koko" application itself.
* There is a single AlbumView user interface for all different models. While applying filter just the model in the view changes. Whereas previously, different models ( ImageFolderModel, ImageTimeModel, ImageLocationModel) have different views

#### List of commits merged into the master branch of the application during GSoC -2017
[Go to Page ](/_pages/2017-08-24-workdone)<br>
[This file](/_pages/workdone.log)

