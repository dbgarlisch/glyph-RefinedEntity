# glyph-InterpolatedEntity
This glyph class wraps an existing structured grid entity and provides access to interpolated grid points.

![InterpolatedEntity Banner Image](../master/docs/images/banner.png  "InterpolatedEntity banner Image")

## Depends On

Project `tcl-Utils`


## Using The Library

To use this class to wrap an existing structured grid entity, you must include
`InterpolatedEntity.glf` in your application script.

```Tcl
  source "/some/path/to/your/copy/of/InterpolatedEntity.glf"
```

Basic usage example.

```Tcl
  Debug setVerbose 1 ;# enable debug messages
  set createPts 0

  # $sblk refers to an exisiting structured block entity
  # $intpBlk provides access to an interpolated grid with a 3x cell density
  set refEnt [pw::InterpolatedEntity new $sblk 3]
  vputs "$intpBlk getEnt            = [$intpBlk getEnt]"
  vputs "$intpBlk getMult           = [$intpBlk getMult]"
  vputs "$intpBlk getOrigDimensions = [$intpBlk getOrigDimensions]"
  vputs "$intpBlk getDimensions     = [$intpBlk getDimensions]"

  lassign [$intpBlk getDimensions] iDim jDim kDim
  for {set ii 1} {$ii <= $iDim} {incr ii} {
    for {set jj 1} {$jj <= $jDim} {incr jj} {
      for {set kk 1} {$kk <= $kDim} {incr kk} {
        set ndx [list $ii $jj $kk]
        set xyz [$intpBlk getXYZ $ndx]
        puts "[list $ndx] ==> $xyz"
        if { $createPts } {
          [pw::Point create] setPoint $xyz
        }
      }
    }
  }

  $intpBlk delete
```

See the [glyph-InterpolatedEntity Class Docs](docs/InterpolatedEntity.md) for full documentation.
