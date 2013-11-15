opensimulator-helper
====================

Very small repository for containing PHP helper code necessary for some transactions involving an economy (e.g. selling land even for $0)

Code originally comes from Melanie Theilker and Teravus Ovares with some cleanup by BlueWall.  Originating version was the opensim-wi
project (http://forge.opensimulator.org/gf/project/opensimwi/)

I will maintain this code but have no current plans to extend it (i.e. I won't develop it into a proper economy module unless someone heavily incentivises it :)

However, patches are welcome.

Background
==========

In the Second Life system (and hence in OpenSimulator), land sales, even for $0, require the viewer to directly interact with a set of 
XMLRPC functions.  The landtool.php in this repository supplies a minimum version of these functions, so that sales can be made for $0.  Sales
for any other amount will probably also work but no actual money transactions will occur (i.e. the sales will still be for free).

Instructions
============

1) Configure landtool.php with a mysql user that can access your OpenSimulator ROBUST databases.  This is required so that the code can
authenticate that requests are coming from valid logged in users.

2) Place landtool.php in a place where it can be accessed via a web-server.  
You will also need PHP to be active with the xmlrpc extension (in Ubuntu this is the package named php5-xmlrpc).

3) Edit the economy parameter in the [GridInfo] section in your bin/Robust.ini OpenSimulator file (or Robust.HG.ini if appropriate) so that it is set
to the webfolder containing landtool.php.  For instance, if landtool.php is accessible via the URL http://example.com/landtool.php, then you will need to configure

[GridInfo]

economy = http://example.com/

Since the viewer is contact this URL directly, it must be accessible to anybody who logs in to your grid.

4) Restart the ROBUST instance hosting the login service.  Users that have previously logged in to your grid with a viewer that records grid URLs
may need to refresh this information.

A user should now be able to buy land.  Please note that on some viewers (e.g. Singularity 1.8.3) you may need to enable the admin menu
(shortcut ctrl+alt+v) before you can buy land, even though you do not need to have admin status.  This may be a viewer bug or OpenSimulator is
not currently supplying the correct information to enable land sales properly.
