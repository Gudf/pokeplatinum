compress_gen = generator(nitrogfx_exe,
    arguments: [ '@INPUT@', '@OUTPUT@', '@EXTRA_ARGS@', ],
    output: '@PLAINNAME@.lz',
)

palettes_nclr = nclr_gen.process(
    files(
        '00000.pal',
        '00003.pal',
        '00007.pal',
        '00011.pal',
        '00012.pal',
        '00016.pal',
        '00019.pal',
        '00023.pal',
        '00029.pal',
        '00032.pal',
        '00036.pal',
        '00040.pal',
        '00045.pal',
    ), 
    extra_args: [
        '-bitdepth', '4'
    ]
)

tiles_sopc_ncgr_comp = ncgr_gen.process(
    files(
        '00001.png',
        '00006.png',
        '00017.png',
        '00022.png',
        '00027.png',
        '00030.png',
    ),
    extra_args: [
        '-version101',
        '-sopc',
    ]
)


tiles_sopc_ncgr_no_comp = ncgr_gen.process(
    files('00044.png'),
    extra_args: ['-version101', '-sopc']
)

tiles_clobbersize_ncgr = ncgr_gen.process(
    files(
        '00010.png',
        '00015.png',
        '00035.png',
        '00039.png',
        '00043.png',
    ),
    extra_args: ['-version101', '-clobbersize']
)

tiles_fixed_size_ncgr = ncgr_gen.process(
    files(
        '00026.png',
    ),
    extra_args: ['-version101', '-clobbersize', '-num_tiles', '581']
)

tilemaps_nscr = copy_gen.process(files(
    '00002.NSCR',
    '00004.NSCR',
    '00005.NSCR',
    '00018.NSCR',
    '00020.NSCR',
    '00021.NSCR',
    '00028.NSCR',
    '00031.NSCR',
))

nanr = nanr_gen.process(files(
    '00008.json',
    '00013.json',
    '00024.json',
    '00033.json',
    '00037.json',
    '00041.json',
    )
)

ncer = ncer_gen.process(files(
        '00009.json',
        '00014.json',
        '00025.json',
        '00034.json',
        '00038.json',
        '00042.json',
    )
)

files_compressed = compress_gen.process(
    tiles_sopc_ncgr_comp,
    tiles_clobbersize_ncgr,
    tiles_fixed_size_ncgr,
    tilemaps_nscr,
    nanr,
    ncer,
    extra_args: ['-nopad']
)

mystery_gift_gra_order = files('mystery_gift_graphics.order')
mystery_gift_gra_ignore = files('mystery_gift_graphics.ignore')

mystery_narc = custom_target('mystery.narc',
    output: [
        'mystery.narc',
        'mystery.naix',
    ],
    input: [
        files_compressed,
        tiles_sopc_ncgr_no_comp,
        palettes_nclr,
        mystery_gift_gra_order,
        mystery_gift_gra_ignore,
    ],
    command: [
        narc_exe, 'create',
        '--naix',
        '--order', mystery_gift_gra_order,
        '--ignore', mystery_gift_gra_ignore,
        '--output', '@OUTPUT0@',
        '@PRIVATE_DIR@'
    ]
)

nitrofs_files += mystery_narc
naix_headers += mystery_narc[1]
