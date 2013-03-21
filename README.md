php5-proj
=========

A php extension for proj.4

Code example (see: [ProjAPI](http://trac.osgeo.org/proj/wiki/ProjAPI)):
-------------
	<?php  
	$pj_merc = pj_init_plus("+proj=merc +ellps=clrk66 +lat_ts=33");  
	$pj_latlong = pj_init_plus("+proj=latlong +ellps=clrk66");  
	if ($pj_merc !== false && $pj_latlong !== false) {  
		$x = deg2rad(-16);  
		$y = deg2rad(20.25);  
		$transformed = pj_transform($pj_merc, $pj_latlong, 1, 1, $x, $y);  
		print 'latitude: '.$transformed['x'].'<br />';  
		print 'longitude: '.$transformed['y'].'<br />';  
	}  
	?>

Output:
-------
latitude: -1495284.2114735  
longitude: 1920596.7899174

API Functions
=============
Basic API
---------
**resource pj_init_plus(string definition);**  
Create a Proj.4 resource coordinate system object from the string definition.  
  
**int pj_transform(resource srcdefn, resource dstdefn, int point_count, int point_offset, double x, double y, double z);**  
Transform the x/y/z points from the source coordinate system to the destination coordinate system.   
  
**void pj_free(resource pj);**  
Frees all resources associated with pj.  

Advanced Functions
------------------
**boolean pj_is_latlong(resource pj);**  
Returns true if the passed coordinate system is geographic (proj=latlong).  
  
**boolean pj_is_geocent(resource pj);**  
Returns true if the coordinate system is geocentric (proj=geocent).  
  
**string pj_get_def(resource pj, int options);**  
Returns the PROJ.4 initialization string suitable for use with pj_init_plus() that would produce this coordinate system, but with the definition expanded as much as possible (for instance +init= and +datum= definitions).  

Environment Functions
---------------------
**string pj_strerrno(int);**  
Returns the error text associated with the passed in error code.  
  
**int pj_get_errno_ref();**  
Returns an integer value that can be used for the pj_strerrno(int) function.  
  
**string pj_get_release();**  
Returns an internal string describing the release version. 
