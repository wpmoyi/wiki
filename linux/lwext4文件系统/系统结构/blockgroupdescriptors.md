[[_TOC_]]
# Block Group Descriptors 块组描述符 
- 块组描述符，每个block group对一个描述信息，由ext4_group_desc数据结构表示，其中描述块block bitmap的block号，inode bitmap的block号，空闲的block数目，空闲的inode数目等信息
- 块组描述符（如果存在）是块组中的第二项。标准配置是每个块组都包含块组描述符表的完整副本，除非设置了sparse_super特征标志。
- 组描述符是记录位图和inode表的位置的方式意味着它们位置可以浮动。在一个块组内，位置固定的数据结构只有超级块和块组描述符表。flex_bg机制利用这一特性将几个块组合并为一个flex组，并将所有组的位图和inode表在flex组的第一个组中连续排列。
~~~
struct ext4_bgroup {
	uint32_t block_bitmap_lo;	    /* Blocks bitmap block */
	uint32_t inode_bitmap_lo;	    /* Inodes bitmap block */
	uint32_t inode_table_first_block_lo; /* Inodes table block */
	uint16_t free_blocks_count_lo;       /* Free blocks count */
	uint16_t free_inodes_count_lo;       /* Free inodes count */
	uint16_t used_dirs_count_lo;	 /* Directories count */
	uint16_t flags;		       /* EXT4_BG_flags (INODE_UNINIT, etc) */
	uint32_t exclude_bitmap_lo;    /* Exclude bitmap for snapshots */
	uint16_t block_bitmap_csum_lo; /* crc32c(s_uuid+grp_num+bbitmap) LE */
	uint16_t inode_bitmap_csum_lo; /* crc32c(s_uuid+grp_num+ibitmap) LE */
	uint16_t itable_unused_lo;     /* Unused inodes count */
	uint16_t checksum;	     /* crc16(sb_uuid+group+desc) */

	uint32_t block_bitmap_hi;	    /* Blocks bitmap block MSB */
	uint32_t inode_bitmap_hi;	    /* I-nodes bitmap block MSB */
	uint32_t inode_table_first_block_hi; /* I-nodes table block MSB */
	uint16_t free_blocks_count_hi;       /* Free blocks count MSB */
	uint16_t free_inodes_count_hi;       /* Free i-nodes count MSB */
	uint16_t used_dirs_count_hi;	 /* Directories count MSB */
	uint16_t itable_unused_hi;	   /* Unused inodes count MSB */
	uint32_t exclude_bitmap_hi;	  /* Exclude bitmap block MSB */
	uint16_t block_bitmap_csum_hi; /* crc32c(s_uuid+grp_num+bbitmap) BE */
	uint16_t inode_bitmap_csum_hi; /* crc32c(s_uuid+grp_num+ibitmap) BE */
	uint32_t reserved;	     /* Padding */
};
~~~