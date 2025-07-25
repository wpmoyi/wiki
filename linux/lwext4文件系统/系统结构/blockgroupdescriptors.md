[[_TOC_]]
# Block Group Descriptors ���������� 
- ������������ÿ��block group��һ��������Ϣ����ext4_group_desc���ݽṹ��ʾ������������block bitmap��block�ţ�inode bitmap��block�ţ����е�block��Ŀ�����е�inode��Ŀ����Ϣ
- ������������������ڣ��ǿ����еĵڶ����׼������ÿ�����鶼�������������������������������������sparse_super������־��
- ���������Ǽ�¼λͼ��inode���λ�õķ�ʽ��ζ������λ�ÿ��Ը�������һ�������ڣ�λ�ù̶������ݽṹֻ�г�����Ϳ�����������flex_bg����������һ���Խ���������ϲ�Ϊһ��flex�飬�����������λͼ��inode����flex��ĵ�һ�������������С�
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