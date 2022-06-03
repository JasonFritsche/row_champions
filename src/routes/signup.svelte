<script>
	import { createForm } from 'felte';
	import { validator } from '@felte/validator-yup';
	import * as yup from 'yup';

	import { Button, Input, Field, Row, Col } from 'svelte-chota';

	const schema = yup.object({
		email: yup.string().email().required(),
		password: yup.string().required('Password is required'),
		passwordConfirmation: yup.string().oneOf([yup.ref('password'), null], 'Passwords must match')
	});

	const { form, errors, touched } = createForm({
		extend: validator({ schema }),
		onSubmit: (values, context) => {
			console.log('values', values);
			console.log('context', context);
		},
		onSuccess: (response, context) => {
			console.log('response', response);
			console.log('context', context);
		},
		onError: (err, context) => {
			console.log('err', err);
			console.log('context', context);
		}
	});
</script>

<div class="signup-component">
	<Row class="is-marginless">
		<Col size="11" sizeMD="5">
			<div>Sign Up</div>
		</Col>
		<Col size="12" sizeMD="6">
			<form class="signup-form" use:form>
				<Field label="Email">
					<Input type="text" name="email" placeholder="your email" />
				</Field>
				<Field label="Password">
					<Input type="password" name="password" placeholder="your password" />
				</Field>
				<Field label="Verify Password">
					<Input type="password" name="passwordConfirmation" placeholder="Verify your password" />
				</Field>
				<Button class="is-full-width" primary type="submit">Sign In</Button>
			</form>
		</Col>
	</Row>
</div>

<!-- <pre>
	{JSON.stringify($errors, null, 2)}
  </pre>

<pre>
	{JSON.stringify($touched, null, 2)}
  </pre> -->
<style>
	.signup-form {
		padding: 1em;
	}
</style>
