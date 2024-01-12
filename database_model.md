SET check_function_bodies = false
;
CREATE TABLE friend(
id serial NOT NULL,
"name" text NOT NULL,
pizza_order_id integer NOT NULL,
CONSTRAINT friend_pkey PRIMARY KEY(id)
);
CREATE TABLE pizza(id serial NOT NULL, title integer NOT NULL);
CREATE TABLE pizza_order(
id serial NOT NULL,
friend_id integer NOT NULL,
pizza_id integer NOT NULL,
CONSTRAINT pizza_order_pkey PRIMARY KEY(id)
);
CREATE TABLE pizza_topping(
id serial NOT NULL,
title text NOT NULL,
emoji text NOT NULL,
available boolean NOT NULL,
pizza_topping_pizza_id integer NOT NULL,
CONSTRAINT pizza_topping_pkey PRIMARY KEY(id)
);
CREATE TABLE pizza_topping_pizza(
id serial NOT NULL,
pizza_id integer NOT NULL,
pizza_topping_id integer NOT NULL,
CONSTRAINT pizza_topping_pizza_pkey PRIMARY KEY(id)
);
ALTER TABLE pizza_topping_pizza
ADD CONSTRAINT pizza_topping_pizza_fkey FOREIGN KEY REFERENCES pizza;
ALTER TABLE pizza_topping
ADD CONSTRAINT pizza_topping_pizza_topping_pizza_id_fkey
FOREIGN KEY (pizza_topping_pizza_id) REFERENCES pizza_topping_pizza (id);
ALTER TABLE pizza_order
ADD CONSTRAINT pizza_order_fkey FOREIGN KEY REFERENCES pizza;
ALTER TABLE friend
ADD CONSTRAINT friend_pizza_order_id_fkey
FOREIGN KEY (pizza_order_id) REFERENCES pizza_order (id);
