# Tevrozo Guidelines for Mobile Development with Flutter

## General Guidelines

### Naming Conventions

1. Ensure the use of proper English when naming.
   - Incorrect: listChurch()
   - Correct: listChurches()
2. Provide suggestions to facilitate future work (e.g., best practices).
3. Avoid preemptively solving future issues.

## Bloc

1. File Naming Convention: `<feature>_bloc.dart`
   - Maintain consistency across files.
2. Class Naming Convention: `<Feature>Bloc`
   - Ensure uniformity in naming.
3. Prefer named parameters consistently.
4. Utilize private parameter names for bloc constructors (e.g., \_<parameter_name>).
   - Facilitates cleaner use-case calls from blocs and ensures consistency in naming conventions throughout the app.
5. While cross-using use-cases of other features in blocs is permitted, refrain from cross-using data fetching use-cases. Utilize the provided provider for such cases, or create one if none exists.

## Providers

- Refer to the documentation on providers before implementation, especially regarding the type of provider to use. [Provider Documentation](https://riverpod.dev/docs/introduction/getting_started#:~:text=Concepts%20%F0%9F%9A%A7-,All%20Providers%20%F0%9F%9A%A7,-Provider)

1. Utilize generated providers whenever feasible.
2. Reserve StateProviders for managing simple states such as boolean values and strings, avoiding their use for custom classes.
3. When folding an `Either` object, use appropriate naming conventions as illustrated in the following example:

   ```dart
   @riverpod
   Future<List<Address>> listAddresses(
     ListAddressesRef ref,
     String postcode,
   ) async {
     final bloc = sl<AddressBloc>();
     final response = await bloc.listAddresses(postcode: postcode);

     return response.fold(
       (failure) => throw failure, // 'failure' indicates the returned failure object
       (addresses) => addresses, // 'addresses' indicates the returned list of addresses
     );
   }
   ```
