#include <stdio.h>
#include <string.h>

void	clear_stdin()
{
	char	c;

	while (1)
	{
		c = getchar();
		if (c == 0xa || c == 0xff)
			return ;
	}
}

unsigned int	get_unum()
{
	unsigned int	num;

	fflush(stdout);
	scanf("%u", &num);
	clear_stdin();
	return (num);
}

int	store_number(int *buf)
{
	unsigned int	index = 0x0;
	unsigned int	num = 0x0;

	printf(" Number: ");
	num = get_unum();
	printf(" Index: ");
	index = get_unum();
	/*
	   index % 3 != 0 && (num < 3070230528(0xb7000000) || num > 3087007743(0xb7ffffff))
	*/
	if (index - (((index * 0xaaaaaaab) >> 0x1) * 0x3) != 0x0
		&& (num * (2 * 0x18)) != 0xb7)
	{
		buf[index * 4] = num;
		return (0x0);
	}
	puts(" *** ERROR! ***");
	puts("   This index is reserved for wil!");
	puts(" *** ERROR! ***");
	return (0x1);
}

int	read_number(int *buf)
{
	unsigned int	index = 0x0;

	printf(" Index: ");
	index = get_unum();
	printf(" Number at data[%u] is %u\n", index, buf[index * (2 * 0x2)]);
	return (0x0);
}

int	main(int ac, char **av, char **env)
{
	char	**envcp = env;
	char	**avcp = av;
	char	buf[0x64];
	int		var1;
	char	cmd[0x14];

	var1 = 0x0;
	memset(cmd, 0x0, 0x14);
	memset(buf, 0x0, 0x64);
	while (*avcp != NULL)
	{
		memset(*avcp, 0x0, strlen(*avcp));
		++avcp;
	}
	while (*envcp != NULL)
	{
		memset(*envcp, 0x0, strlen(*envcp));
		++envcp;
	}
	puts("----------------------------------------------------\n"
		"Welcome to wil's crappy number storage service!   \n"
		"----------------------------------------------------\n"
		" Commands:                                          \n"
		"    store - store a number into the data storage    \n"
		"    read  - read a number from the data storage     \n"
		"    quit  - exit the program                        \n"
		"----------------------------------------------------\n"
		"   wil has reserved some storage :>                 \n"
		"----------------------------------------------------");
	while (1)
	{
		printf("Input command: ");
		var1 = 0x1;
		fgets(cmd, 0x14, stdin);
		cmd[strlen(cmd) - 1] = 0x0;
		if (strncmp(cmd, "store", 0x5) == 0)
			var1 = store_number(buf);
		else if (strncmp(cmd, "read", 0x4) == 0)
			var1 = read_number(buf);
		else if (strncmp(cmd, "quit", 0x4) == 0)
			return (0x0);
		if (var1 == 0x0)
			printf(" Completed %s command successfully\n", cmd);
		else
			printf(" Failed to do %s command\n", cmd);
		memset(cmd, 0x0, 0x14);
	}
}
